# AWS Installation

This guide covers what you need to provide to install DuploCloud AI Helpdesk on AWS and what DuploCloud will set up in your environment.

***

## Overview

The installation deploys the following components into a dedicated namespace in your Kubernetes cluster:

| Component              | Description                                                      |
| ---------------------- | ---------------------------------------------------------------- |
| **Backend**            | ASP.NET Core API server — tickets, projects, agent orchestration |
| **Frontend**           | React web UI served via nginx                                    |
| **MongoDB**            | Embedded database (Kubernetes StatefulSet)                       |
| **Web Terminal**       | Browser-based terminal for agent command execution               |
| **Duplo Agent**        | Claude-powered AI agent runtime                                  |
| **MCP Server**         | Model Context Protocol server for tool integrations              |
| **Ingress (ALB)**      | AWS Application Load Balancer routing HTTPS traffic              |
| **Persistent Storage** | EFS-backed shared volume for agent working directories           |

All components run entirely within your AWS account.&#x20;

***

## Deployment Scenarios

### Ideal: Fresh AWS Account (Recommended)

The cleanest path is to provide a **dedicated, empty AWS account** for DuploCloud AI HelpDesk. This gives DuploCloud full control to create all required infrastructure from scratch — VPC, EKS cluster, EFS, security groups, ACM certificates — with no risk of conflicting with existing workloads.

**What you do:**

1. Create a new AWS account (or sub-account in your AWS Organization)
2. Create an IAM user with full admin access and share the credentials with DuploCloud
3. DuploCloud handles everything from there

This is the fastest path to a clean, reproducible installation.

***

### Alternative: Existing AWS Account

If you prefer to install into an existing AWS account (e.g. alongside other workloads), this is fully supported. DuploCloud HelpDesk deploys into a dedicated Kubernetes namespace and does not modify any resource that was created outside of Duplo.

**What you need to ensure:**

* An existing EKS cluster with available node capacity
* A VPC with public subnets for the ALB
* Permission to create EFS, security groups, and ACM certificates in the account

***

## Installation Requirements&#x20;

In either of the scenarios above, we will need:&#x20;

### 1. AWS Access

| Item                              | Required | Notes                                                                                |
| --------------------------------- | -------- | ------------------------------------------------------------------------------------ |
| AWS Account ID                    | ✅        | 12-digit number (e.g. `774157348504`)                                                |
| IAM credentials for the installer | ✅        | See [Granting Installer Access](aws-installation.md#granting-installer-access) below |
| Target AWS region                 | ✅        | e.g. `us-east-1`                                                                     |

### 2. Kubernetes Cluster

| Item                    | Required | Notes                                  |
| ----------------------- | -------- | -------------------------------------- |
| EKS cluster             | ✅        | Kubernetes v1.21+                      |
| Available node capacity | ✅        | Minimum 2 nodes, `t3a.large` or larger |

> **No cluster yet?** If you don't have an EKS cluster, DuploCloud will create one. Full admin access to the account is required for this.

> **Sharing a cluster:** Multiple applications can coexist in the same EKS cluster — each runs in its own namespace. HelpDesk deploys into `duploservices-<name>` by default.

### 3. Domain and DNS

| Item                               | Required | Notes                                                                                                         |
| ---------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------- |
| Domain or subdomain for the portal | ✅        | e.g. `helpdesk.yourcompany.com` — does not need to be publicly accessible; a private hosted zone is supported |
| xterm subdomain                    | ✅        | e.g. `xterm.helpdesk.yourcompany.com`                                                                         |
| Access to DNS provider             | ✅        | Route 53, Cloudflare, or equivalent                                                                           |
| Existing ACM certificate           | Optional | If not available, one will be requested during install                                                        |

### 4. Administrator Emails

| Item                  | Required | Notes                                                     |
| --------------------- | -------- | --------------------------------------------------------- |
| Super-user email list | ✅        | Comma-separated, e.g. `admin@company.com,ops@company.com` |

These accounts receive full administrative access to DuploCloud after installation.

***

## Granting Installer Access

DuploCloud requires full admin access to your AWS account to perform the installation — this is needed to create the VPC, EKS cluster, EFS, load balancer, security groups, and ACM certificates.

The recommended approach is to create a dedicated IAM user with `AdministratorAccess` and share the credentials securely with DuploCloud:

1. In the AWS Console → **IAM** → **Users** → **Create user**
2. Name it `duplocloud-installer` (or similar)
3. Attach the `AdministratorAccess` policy directly
4. Under **Security credentials** → create an **Access Key** (for CLI use)
5. Share the Access Key ID and Secret Access Key with DuploCloud

Alternatively, if your organization uses IAM roles, you can create a role with `AdministratorAccess` and add DuploCloud's IAM identity as a trusted principal so we can assume it. DuploCloud will confirm the exact trust policy configuration.

> **After installation:** Access can be revoked by deleting the IAM user or role. If you require tighter permission scoping, contact DuploCloud — scoped IAM policies are available for environments where full admin access is not permitted.

***

## Connecting AWS to DuploCloud (Post-Installation)

Once the portal is live, you can connect AWS accounts to it so the AI agent can query and manage your infrastructure. This uses the **AWS Cloud Provider** feature inside the HelpDesk.

> Use the [CloudFormation Template](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/review?templateURL=https://duploservices-ai-access-227120241369.s3.us-west-2.amazonaws.com/aws.yaml) to automatically create the IAM role needed to connect an AWS account to HelpDesk. You can also [download the template](https://duploservices-ai-access-227120241369.s3.us-west-2.amazonaws.com/aws.yaml) for review.

The `HelpdeskAccountId` parameter in the template is the AWS account ID **where Helpdesk is deployed**. This configures the IAM trust policy so the HelpDesk service can assume the created role and manage resources in your AWS accounts.

There are two authentication methods:

### IAM Role (Recommended)

1. Log in to the Helpdesk portal → **Providers** → select your tenant → **Cloud** tab → **+ Add**
2. Fill in **Name**, **Type** = `AWS`, **Account ID**
3. Go to the **Credentials** tab → **+ Add** → **Credential Type** = `IAM Role`
4. Enter the **IAM Role ARN** to assume
5. Add a **Scope** — select region and resource types
6. Use the scope in a ticket to have the agent act on your AWS account

### Access Key

1. Follow steps 1–2 above to create a provider
2. Go to **Credentials** → **+ Add** → **Credential Type** = `Access Key`
3. Enter the Access Key ID and Secret Access Key
4. Add a **Scope** and use it in tickets

For full step-by-step screenshots, see the [AWS Provider guide](../integrating-providers/amazon-web-services-aws.md).

***

## Troubleshooting

| Issue                                  | Resolution                                                                                                    |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| EFS mount targets not available        | Wait up to 10 minutes — EFS creates one mount target per subnet                                               |
| ALB not provisioned                    | Verify AWS Load Balancer Controller is installed: `kubectl get pods -n kube-system \| grep aws-load-balancer` |
| Pods stuck in `Pending`                | Check EFS CSI driver: `kubectl get pods -n kube-system \| grep efs`                                           |
| ACM cert stuck in `PENDING_VALIDATION` | DNS validation CNAME records have not been added or have not propagated yet                                   |
