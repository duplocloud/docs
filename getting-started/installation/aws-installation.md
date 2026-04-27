# AWS Installation Guide

This guide covers everything required to install DuploCloud AI Helpdesk on AWS in **Standalone mode** — running independently in your own EKS cluster, without a DuploCloud master portal.

---

## Overview

The installation deploys the following components into a dedicated namespace in your Kubernetes cluster:

| Component | Description |
|---|---|
| **Backend** | ASP.NET Core API server — tickets, projects, agent orchestration |
| **Frontend** | React web UI served via nginx |
| **MongoDB** | Embedded database (Kubernetes StatefulSet) |
| **Web Terminal** | Browser-based terminal for agent command execution |
| **Duplo Agent** | Claude-powered AI agent runtime |
| **Ingress (ALB)** | AWS Application Load Balancer routing HTTPS traffic |
| **Persistent Storage** | EFS-backed shared volume for agent working directories |

All components run entirely within your AWS account. DuploCloud does not operate any shared infrastructure on your behalf.

---

## Deployment Scenarios

### Ideal: Fresh AWS Account (Recommended)

The cleanest path is for the customer to provide a **dedicated, empty AWS account** for DuploCloud AI Helpdesk. This gives our team full control to create all required infrastructure from scratch — VPC, EKS cluster, EFS, security groups, ACM certificates — with no risk of conflicting with existing workloads.

**What the customer does:**
1. Creates a new AWS account (or sub-account in their AWS Organization)
2. Runs the [CloudFormation template](#granting-installer-access-via-cloudformation) to create an installer role
3. Sends DuploCloud the Role ARN and account ID

This is the fastest path to a clean, reproducible installation.

---

### Alternative: Existing Production Account

If the customer prefers to install into an existing AWS account (e.g. alongside other workloads), this is fully supported. DuploCloud Helpdesk deploys into a dedicated Kubernetes namespace and does not modify existing resources outside of that namespace.

**What the customer needs to ensure:**
- An existing EKS cluster with available node capacity
- A VPC with public subnets for the ALB
- Permission to create EFS, security groups, and ACM certificates in the account

> **Sharing a cluster is fine** — multiple applications can coexist in the same EKS cluster. Each runs in its own namespace. Helpdesk deploys into `duploservices-<tenantName>` by default.

---

## Prerequisites

### Tools (DuploCloud Team)

The following must be installed on the machine performing the installation:

| Tool | Version | Install |
|---|---|---|
| `aws` CLI | v2+ | `brew install awscli` |
| `kubectl` | v1.21+ | `brew install kubectl` |
| `helm` | v3+ | `brew install helm` |
| `python3` | v3.7+ | Built-in on macOS |

Verify all tools are installed before starting:
```bash
aws --version
kubectl version --client
helm version --short
```

---

## What the Customer Must Provide

Before scheduling the installation, collect the following from the customer. Items marked **Required** must be in place before the installation begins.

### 1. AWS Access

| Item | Required | Notes |
|---|---|---|
| AWS Account ID | ✅ | 12-digit number (e.g. `774157348504`) |
| IAM credentials for the installer | ✅ | See [IAM Policy](#iam-policy-for-the-installer) below |
| Target AWS region | ✅ | e.g. `us-east-1` |

The recommended way to grant access is via the [CloudFormation template](#granting-installer-access-via-cloudformation) — the customer runs it once and shares the output Role ARN. Alternatively, the customer can provide static IAM credentials directly.

### 2. Kubernetes Cluster

| Item | Required | Notes |
|---|---|---|
| Existing EKS cluster | ✅ | Kubernetes v1.21+ |
| Kubeconfig access to the cluster | ✅ | Or an IAM role with `eks:DescribeCluster` to generate one |
| Available node capacity | ✅ | Minimum 2 nodes, `t3a.large` or larger |

> **No cluster yet?** If the customer does not have an EKS cluster, one must be created before installation. See [IAM Policy Without an Existing EKS Cluster](#without-an-existing-eks-cluster-additional-permissions) for the additional permissions required.

> **Sharing a cluster:** Multiple applications can coexist in the same EKS cluster — each runs in its own namespace. Helpdesk deploys into `duploservices-<tenantName>` by default.

### 3. Domain and DNS

| Item | Required | Notes |
|---|---|---|
| Domain or subdomain for the portal | ✅ | e.g. `helpdesk.yourcompany.com` |
| xterm subdomain | ✅ | e.g. `xterm.helpdesk.yourcompany.com` |
| Access to DNS provider | ✅ | Route 53, Cloudflare, or equivalent |
| Existing ACM certificate | Optional | If not available, one will be requested during install |

DNS is configured in **two phases** during the installation:
1. **Before deployment** — a CNAME record is added to validate the ACM certificate (DNS validation)
2. **After deployment** — a CNAME or Alias A record points the domain to the provisioned ALB

### 4. Google OAuth Credentials

DuploCloud AI Helpdesk uses Google OAuth for user authentication. Username/password login is not supported.

| Item | Required | Notes |
|---|---|---|
| Google OAuth Client ID | ✅ | Created in Google Cloud Console |
| Google OAuth Client Secret | ✅ | Created in Google Cloud Console |

To create these:
1. Go to [Google Cloud Console](https://console.cloud.google.com) → **APIs & Services** → **Credentials**
2. Click **Create Credentials** → **OAuth 2.0 Client ID**
3. Application type: **Web application**
4. Add the portal URL to **Authorized JavaScript origins** (e.g. `https://helpdesk.yourcompany.com`)
5. Add `https://helpdesk.yourcompany.com/auth/callback` to **Authorized redirect URIs**
6. Copy the Client ID and Client Secret

> Users log in with any Google account (Gmail or Google Workspace). Admin access is controlled by the super-user email list.

### 5. Administrator Emails

| Item | Required | Notes |
|---|---|---|
| Super-user email list | ✅ | Comma-separated, e.g. `admin@company.com,ops@company.com` |

These accounts receive full administrative access after installation.

### 6. Slack Integration (Optional)

| Item | Required | Notes |
|---|---|---|
| Slack App Token (`xapp-...`) | Optional | Only if enabling Slack backend integration |
| Slack Bot Token (`xoxb-...`) | Optional | Only if enabling Slack backend integration |

---

## Granting Installer Access via CloudFormation

### When to Use This Template

The CloudFormation template is the **recommended access method for all customer deployments** — both fresh AWS accounts and existing accounts with an EKS cluster already in place.

Use it when:
- **Fresh AWS account** — the customer is providing a new, dedicated account for the Helpdesk installation. DuploCloud will create all infrastructure (VPC, EKS cluster, EFS, ALB, etc.) from scratch using the admin role.
- **Existing EKS cluster** — the customer already has an EKS cluster. The template creates both an AWS admin role (for provisioning supporting resources) and an EKS admin role (for kubectl access to the cluster).
- **Audit trail preferred** — the template and its created roles are visible in CloudFormation and IAM, making it easy for the customer to review what was created and remove access later by deleting the stack.

The only alternative is manually creating IAM policies (see [Reference: Minimum IAM Policies](#reference-minimum-iam-policies-manual-alternative) below), which is appropriate only if the customer's security policy prohibits running CloudFormation.

---

### How Cross-Account Access Works

The template creates IAM roles in the **customer's** AWS account. Each role includes a **trust policy** that allows DuploCloud's AWS account to assume the role via `sts:AssumeRole`.

The `HelpdeskAccountId` parameter is DuploCloud's AWS account ID — setting it is what establishes this cross-account trust relationship. Without it, the created roles could only be assumed by principals within the customer's own account, which would not grant DuploCloud access.

Once the roles are created, our team assumes them from our own AWS account using a local `~/.aws/config` profile — no long-lived credentials are ever shared with DuploCloud.

---

### What the Template Creates

The template can create up to four IAM roles, all conditional on parameters:

| Role Name | AWS Policy Attached | Purpose |
|---|---|---|
| `DuploCloud-AWS-Admin` | `AdministratorAccess` | Full AWS access — creates VPC, EKS, EFS, ALB, ACM, etc. |
| `DuploCloud-AWS-ReadOnly` | `ReadOnlyAccess` | Read-only AWS access — for audits or monitoring without write permissions |
| `DuploCloud-EKS-Admin-<ClusterName>` | `AmazonEKSClusterAdminPolicy` | Full `cluster-admin` kubectl access to a specific EKS cluster |
| `DuploCloud-EKS-ReadOnly-<ClusterName>` | `AmazonEKSViewPolicy` | Read-only kubectl access to a specific EKS cluster |

All roles trust the same `HelpdeskAccountId` (DuploCloud's account).

---

### Step 1 — Deploy the CloudFormation Template

Ask the customer to open this link in the AWS Console (or send it to them):

> [Launch CloudFormation Stack](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/review?templateURL=https://duploservices-ai-access-227120241369.s3.us-west-2.amazonaws.com/aws.yaml)

You can also [download the template](https://duploservices-ai-access-227120241369.s3.us-west-2.amazonaws.com/aws.yaml) to review before running it.

### Step 2 — Set the Parameters

| Parameter | Default | Recommended for Installation | Notes |
|---|---|---|---|
| `CreateAdminRole` | false | **true** | Creates `DuploCloud-AWS-Admin` with `AdministratorAccess` — required for all installations |
| `CreateReadOnlyRole` | false | false | Creates `DuploCloud-AWS-ReadOnly` with `ReadOnlyAccess` — only needed if DuploCloud needs ongoing read-only monitoring access |
| `CreateEKSAdminRole` | false | **true** if cluster exists | Creates `DuploCloud-EKS-Admin-<ClusterName>` with full kubectl access — required if an EKS cluster already exists |
| `CreateEKSReadOnlyRole` | false | false | Creates `DuploCloud-EKS-ReadOnly-<ClusterName>` with read-only kubectl access — not needed for installation |
| `ClusterName` | *(empty)* | `<eks-cluster-name>` if applicable | Required when either EKS role is enabled; must match the exact EKS cluster name |
| `HelpdeskAccountId` | *(empty)* | **DuploCloud's account ID** | Sets the cross-account trust policy — DuploCloud will provide this value |

**Typical configurations:**

| Scenario | Parameters to Enable |
|---|---|
| Fresh AWS account (no EKS yet) | `CreateAdminRole = true`, `HelpdeskAccountId = <duplo-account-id>` |
| Existing EKS cluster | `CreateAdminRole = true`, `CreateEKSAdminRole = true`, `ClusterName = <cluster-name>`, `HelpdeskAccountId = <duplo-account-id>` |

> **No existing EKS cluster?** Leave `CreateEKSAdminRole` as false. The EKS cluster and VPC will be created during installation using the admin role.

### Step 3 — Share the Role ARNs

Once the stack status shows `CREATE_COMPLETE`, the customer opens the stack **Outputs** tab and shares the relevant ARNs:

- `AdminRoleArn` — e.g. `arn:aws:iam::123456789012:role/DuploCloud-AWS-Admin`
- `EKSAdminRoleArn` — e.g. `arn:aws:iam::123456789012:role/DuploCloud-EKS-Admin-my-cluster` (if applicable)

### Step 4 — Configure the Installer Profile

Add the role to `~/.aws/config` on the installer machine:

```ini
[profile helpdesk-installer]
role_arn = arn:aws:iam::<CUSTOMER_ACCOUNT_ID>:role/DuploCloud-AWS-Admin
source_profile = <your-base-profile>
region = <target-region>
```

Verify it works:
```bash
aws sts get-caller-identity --profile helpdesk-installer
```

### Revoking Access After Installation

To revoke DuploCloud's access, the customer simply **deletes the CloudFormation stack**. This removes all created IAM roles and their trust policies. No other cleanup is needed.

---

### Reference: Minimum IAM Policies (Manual Alternative)

If the customer cannot run CloudFormation, the following policies can be created manually. Use these as a reference or share them with the customer's AWS administrator.

**With an existing EKS cluster:**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "STSCheck",
      "Effect": "Allow",
      "Action": ["sts:GetCallerIdentity"],
      "Resource": "*"
    },
    {
      "Sid": "EKSAccess",
      "Effect": "Allow",
      "Action": ["eks:DescribeCluster", "eks:ListClusters"],
      "Resource": "*"
    },
    {
      "Sid": "EC2ReadOnly",
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeVpcs", "ec2:DescribeSubnets",
        "ec2:DescribeSecurityGroups", "ec2:DescribeInstances"
      ],
      "Resource": "*"
    },
    {
      "Sid": "EC2SecurityGroupWrite",
      "Effect": "Allow",
      "Action": ["ec2:CreateSecurityGroup", "ec2:AuthorizeSecurityGroupIngress"],
      "Resource": "*"
    },
    {
      "Sid": "ACM",
      "Effect": "Allow",
      "Action": ["acm:ListCertificates", "acm:RequestCertificate", "acm:DescribeCertificate"],
      "Resource": "*"
    },
    {
      "Sid": "EFS",
      "Effect": "Allow",
      "Action": [
        "efs:CreateFileSystem", "efs:DescribeFileSystems",
        "efs:DescribeMountTargets", "efs:TagResource"
      ],
      "Resource": "*"
    }
  ]
}
```

**Without an existing EKS cluster** — add these additional statements to the policy above:

```json
{
  "Sid": "EKSCreate",
  "Effect": "Allow",
  "Action": [
    "eks:CreateCluster", "eks:CreateNodegroup", "eks:UpdateClusterConfig",
    "eks:UpdateNodegroupConfig", "eks:TagResource", "eks:DescribeNodegroup",
    "eks:ListNodegroups", "eks:DescribeUpdate"
  ],
  "Resource": "*"
},
{
  "Sid": "EC2VPCCreate",
  "Effect": "Allow",
  "Action": [
    "ec2:CreateVpc", "ec2:CreateSubnet", "ec2:CreateInternetGateway",
    "ec2:AttachInternetGateway", "ec2:CreateRouteTable", "ec2:CreateRoute",
    "ec2:AssociateRouteTable", "ec2:AllocateAddress", "ec2:CreateNatGateway",
    "ec2:ModifyVpcAttribute", "ec2:ModifySubnetAttribute", "ec2:CreateTags",
    "ec2:DescribeRouteTables", "ec2:DescribeInternetGateways",
    "ec2:DescribeNatGateways", "ec2:DescribeAddresses", "ec2:DescribeAvailabilityZones"
  ],
  "Resource": "*"
},
{
  "Sid": "IAMForEKS",
  "Effect": "Allow",
  "Action": [
    "iam:CreateRole", "iam:AttachRolePolicy", "iam:DetachRolePolicy",
    "iam:PassRole", "iam:GetRole", "iam:ListAttachedRolePolicies",
    "iam:CreateOpenIDConnectProvider", "iam:GetOpenIDConnectProvider"
  ],
  "Resource": "*"
},
{
  "Sid": "AutoScaling",
  "Effect": "Allow",
  "Action": [
    "autoscaling:CreateAutoScalingGroup", "autoscaling:DescribeAutoScalingGroups",
    "autoscaling:UpdateAutoScalingGroup", "autoscaling:CreateLaunchConfiguration",
    "autoscaling:DescribeLaunchConfigurations"
  ],
  "Resource": "*"
}
```

---

## Setting Up an AWS Profile

### Option A — Static IAM Credentials

If the customer provides an access key and secret:

```bash
aws configure --profile <profile-name>
```

You will be prompted for:
- AWS Access Key ID
- AWS Secret Access Key
- Default region (e.g. `us-east-1`)
- Output format (`json`)

Verify the profile works:
```bash
aws sts get-caller-identity --profile <profile-name>
```

### Option B — IAM Role Assumption

If the customer provides a role ARN for you to assume from an existing profile, add this to `~/.aws/config`:

```ini
[profile helpdesk-installer]
role_arn = arn:aws:iam::<ACCOUNT_ID>:role/<ROLE_NAME>
source_profile = <your-base-profile>
region = us-east-1
```

The customer's IAM role must include your IAM user/identity as a trusted principal in its trust policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<YOUR_ACCOUNT_ID>:user/<YOUR_USERNAME>"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

Verify role assumption:
```bash
aws sts get-caller-identity --profile helpdesk-installer
```

---

## Setting Up kubectl Access

Once AWS credentials are configured, generate a kubeconfig for the target EKS cluster:

```bash
aws eks update-kubeconfig \
  --name <cluster-name> \
  --region <region> \
  --profile <profile-name> \
  --alias <friendly-name>
```

Verify connectivity:
```bash
kubectl get nodes
```

You should see the cluster nodes listed with `Ready` status before proceeding.

---

## Installation Methods

There are two ways to install DuploCloud AI Helpdesk on AWS.

---

### Method 1 — Guided Installation via Claude Code Skill (Recommended)

The `helpdesk-install-skill` is a Claude Code skill that guides you interactively through the entire installation. It handles AWS resource discovery, values file generation, and Helm deployment — prompting you at each step and validating inputs against live AWS data.

**Prerequisites:**
- Claude Code CLI installed (`npm install -g @anthropic-ai/claude-code`)
- The `ai-ops` repository cloned locally (the skill lives in `.claude/skills/`)

**Start the installation:**

```bash
cd /path/to/ai-ops
claude
```

Then invoke the skill:

```
/helpdesk-install-skill
```

The skill will walk you through:

1. **Prerequisites check** — verifies `aws`, `kubectl`, `helm` are installed
2. **AWS profile selection** — selects and validates credentials
3. **Kubernetes context selection** — selects and verifies cluster connectivity
4. **Deployment mode** — select `STANDALONE`
5. **Configuration collection** — gathers all required values in grouped prompts
6. **AWS resource discovery** — queries your account for existing VPCs, subnets, security groups, certificates, and storage classes; creates missing resources where needed
7. **Values file generation** — produces `<customerName>-values.yaml` with all substituted values (secrets auto-generated)
8. **Helm deployment** — deploys via local `helm install` or saves values file for manual deployment
9. **Slack notification** — notifies `#customer-ai-deploys` on completion

> **Note:** Add `*-values.yaml` to `.gitignore` — the generated file contains plaintext secrets including MongoDB password and JWT secret.

---

### Method 2 — Manual Helm Deployment

If you already have a values file or prefer to deploy manually:

**Step 1 — Fetch the latest chart version:**

```bash
helm pull oci://quay.io/duplocloud/helpdesk --untar --untardir /tmp/helpdesk-chart
grep "^version:" /tmp/helpdesk-chart/helpdesk/Chart.yaml
```

**Step 2 — Create your values file** based on the template in `ai-ops/.claude/skills/helpdesk-install-skill/values-template.yaml`, substituting all `{{placeholder}}` values.

**Step 3 — Deploy:**

```bash
helm upgrade --install helpdesk oci://quay.io/duplocloud/helpdesk \
  --version <chart-version> \
  --namespace duploservices-<tenantName> \
  --create-namespace \
  --values <customerName>-values.yaml \
  --wait \
  --timeout 10m
```

**Step 4 — Verify:**

```bash
kubectl get pods -n duploservices-<tenantName>
kubectl get ingress -n duploservices-<tenantName>
```

---

## Post-Installation DNS Setup

After the ALB is provisioned, point your domain to it:

**Get the ALB DNS name:**

```bash
kubectl get ingress -n duploservices-<tenantName> \
  -o jsonpath='{.items[0].status.loadBalancer.ingress[0].hostname}'
```

**Add a DNS record at your provider:**

| Type | Name | Value |
|---|---|---|
| CNAME | `helpdesk.yourcompany.com` | `<alb-dns>.us-east-1.elb.amazonaws.com` |
| CNAME | `xterm.helpdesk.yourcompany.com` | `<alb-dns>.us-east-1.elb.amazonaws.com` |

If using **Route 53**, you can use an Alias A record instead of a CNAME, which avoids the extra DNS hop.

---

## Connecting AWS to the Helpdesk (Post-Installation)

Once the portal is live, you can connect AWS accounts to it so AI agents can query and manage your infrastructure. This uses the **AWS Cloud Provider** feature inside the Helpdesk.

> Use the [CloudFormation Template](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/review?templateURL=https://duploservices-ai-access-227120241369.s3.us-west-2.amazonaws.com/aws.yaml) to automatically create the IAM role and Kubernetes credentials needed to connect an AWS account. You can also [download the template](https://duploservices-ai-access-227120241369.s3.us-west-2.amazonaws.com/aws.yaml) for review. For more details, see the [GitHub repo](https://github.com/duplocloud/duplocloud-helpdesk-access).

There are two authentication methods:

### IAM Role (Recommended)

1. Log in to the Helpdesk portal → **Providers** → select your tenant → **Cloud** tab → **+ Add**
2. Fill in **Name**, **Type** = `AWS`, **Account ID**
3. Go to the **Credentials** tab → **+ Add** → **Credential Type** = `IAM Role`
4. Enter the **IAM Role ARN** to assume
5. Add a **Scope** — select region and resource types
6. Use the scope in a ticket to have the agent act on your AWS account

> The IAM role must include the DuploCloud service account as a trusted principal in its trust policy.

### Access Key

1. Follow steps 1–2 above to create a provider
2. Go to **Credentials** → **+ Add** → **Credential Type** = `Access Key`
3. Enter the Access Key ID and Secret Access Key
4. Add a **Scope** and use it in tickets

For full step-by-step screenshots, see the [AWS Provider guide](../integrating-providers/amazon-web-services-aws.md).

---

## Troubleshooting

| Issue | Resolution |
|---|---|
| `aws sts get-caller-identity` fails | Credentials expired or profile misconfigured — re-run `aws configure --profile <name>` |
| `kubectl get nodes` fails | Run `aws eks update-kubeconfig --name <cluster> --region <region> --profile <profile>` |
| EFS mount targets not available | Wait up to 10 minutes — EFS creates one mount target per subnet |
| ALB not provisioned | Verify AWS Load Balancer Controller is installed: `kubectl get pods -n kube-system | grep aws-load-balancer` |
| Pods stuck in `Pending` | Check EFS CSI driver: `kubectl get pods -n kube-system | grep efs` |
| Helm timeout | Check pod events: `kubectl describe pods -n duploservices-<tenantName>` and `kubectl get events -n duploservices-<tenantName> --sort-by='.lastTimestamp'` |
| ACM cert stuck in `PENDING_VALIDATION` | DNS validation CNAME records have not been added or have not propagated yet |
