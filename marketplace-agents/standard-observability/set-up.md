---
description: What you need before you start, how to activate Standard Observability from the Agent Marketplace, and how to connect it to your accounts.
---

# Set Up

## Before you start

- An **EKS cluster** with **FluxCD** and the **AWS Load Balancer Controller** running. The wizard checks these for you on the Cluster Add-ons step.
- Optional on the cluster: the **cluster autoscaler**, and **external-dns** if you want DNS records created for you.
- An **AWS scope** whose IAM identity has the permissions listed below.
- A **Kubernetes scope** for the cluster (needed in both modes, to check add-ons and to apply Kubernetes objects).
- In DevOps extension mode: an **Environment** and **Resource Group** in the workspace (existing, or created by the wizard), and a **Network Baseline** and **Kubernetes cluster** if the wizard must create the Resource Group.
- An **ACM certificate** in the cluster's region that covers the Grafana hostname (and the internal Loki hostname, if you turn that on).
- A **DNS zone** you control for the Grafana hostname (`<prefix>.<DNS suffix>`).
- A default **StorageClass** on the cluster for the Loki, Grafana and Prometheus volumes.
- **Permissions** for the people who will use it (see [Permissions and Safety](permissions-and-safety.md)).

{% hint style="info" %}
If something required is missing, provisioning fails early and tells you what. The S3 VPC endpoint is checked first, before anything is created.
{% endhint %}

<!-- VERIFY: "default StorageClass" is a warning, not a failure, in the code (volumes stay Pending until one is marked default). Confirm the wording you want here. -->

### AWS permissions by feature

The code and README name these actions. In DevOps extension mode some work (node pool, S3 bucket, load balancers) goes through the DuploCloud platform with the scope's role; in standalone mode the AWS CLI makes the calls directly.

| Feature | AWS actions | Mode |
| --- | --- | --- |
| Identify the account | `sts:GetCallerIdentity` | Standalone |
| Read the cluster | `eks:DescribeCluster` | Both |
| S3 gateway VPC endpoint (mandatory) | `ec2:DescribeInstances`, `ec2:DescribeRouteTables`, `ec2:DescribeVpcEndpoints`, `ec2:CreateVpcEndpoint`, `ec2:ModifyVpcEndpoint` | Both |
| Node networking (security group rules) | `ec2:DescribeSecurityGroupRules`, `ec2:AuthorizeSecurityGroupIngress` (also `ec2:DescribeInstances`, `eks:DescribeCluster`) | Both |
| Observability node pool | `eks:CreateNodegroup`, `eks:DescribeNodegroup`, `eks:DeleteNodegroup`, `ec2:DescribeSubnets`, `ec2:DescribeRouteTables` | Standalone |
| Node IAM role (if you do not supply one) | `iam:GetRole`, `iam:CreateRole`, `iam:AttachRolePolicy`, `iam:DetachRolePolicy`, `iam:DeleteRole` | Standalone |
| Log bucket | `s3:CreateBucket`, `s3:ListBucket` (existence check), `s3:PutBucketPublicAccessBlock`, `s3:PutEncryptionConfiguration` | Standalone |
| Workload identity for Loki (IRSA) | `iam:ListOpenIDConnectProviders`, `iam:CreateOpenIDConnectProvider`, `iam:GetRole`, `iam:CreateRole`, `iam:UpdateAssumeRolePolicy`, `iam:PutRolePolicy`, `iam:DeleteRolePolicy` | Standalone |
| Browse certificates and clusters in the wizard | read-only ACM and EKS list calls made by the platform with the AWS scope | Both |

<!-- VERIFY: the list is derived from the AWS CLI calls in the provisioning script and the extension README, not from a published policy. A CloudFormation role template is planned (sub-ticket) and does not exist in the repo. Confirm the full list, including iam:PassRole for the node role, iam:TagRole, S3 permissions for the platform-created bucket, and the ACM list permission. -->
<!-- VERIFY: QA on 2026-11-18 also needed Route 53 record-set permissions and iam:UpdateAssumeRolePolicy. UpdateAssumeRolePolicy is in the standalone code (see table). Route 53 is NOT called by the extension itself; it is used by external-dns on the cluster (and possibly the platform). Confirm who needs it and on which identity. -->
<!-- VERIFY: the QA S3 role named like <infra>-observability-s3 matches the standalone role name {cluster}-observability-s3. Confirm what the DevOps mode role is called. -->

### Permissions on the cluster and for DNS

- The Kubernetes scope's identity applies Flux Helm objects, Secrets, a service account, Ingresses, a NetworkPolicy and a Namespace in the stack's namespace, and reads cluster add-ons.
- If you choose **Create it automatically (external-dns)** for DNS, external-dns on the cluster creates the record in Route 53, so the cluster's external-dns identity needs permission on the zone. If you choose **I will create it**, you create the record yourself.

<!-- VERIFY: exact Kubernetes RBAC the Kubernetes scope needs. The repo only says the scope applies the objects; it lists no least-privilege role. -->

### One-time setup for Grafana sign-in

DuploCloud hands users to Grafana through its Authenticate URL page, which only posts the user's session to allow-listed hosts. A DuploCloud **Administrator** must add the Grafana host once per stack: **Administrator > System Settings > System Config**, type `AppConfig/otel`, value `https://<grafana hostname>`. Without it the browser stops at "Redirecting to .../duplo_auth/bridge".

<!-- VERIFY: menu path and setting name come from the extension README. Confirm in QA and whether this is still needed in the released version. Screenshot SO-12. -->

## Activate Standard Observability

1. Open the **Agent Marketplace** and find **Standard Observability**.
2. Select **Activate** and confirm.
3. When it finishes, **Observability > Standard Observability** appears in the menu.

<!-- VERIFY: marketplace steps and button names are not in the repo. The menu path comes from the extension manifest: section "Observability", item "Standard Observability". The README also mentions "Observability > Monitoring"; the manifest has no such item (the Monitoring page is a route of the same item). Screenshots SO-01 and SO-02. -->

## Grant access

Give the people who will use it the permissions described in [Permissions and Safety](permissions-and-safety.md). Creating the Grafana scope and the Grafana sign-in allow-list entry also need a DuploCloud Administrator.

## Create your first stack

1. Open **Observability > Standard Observability**. With no stack yet you see **Create Observability Stack**.
2. Follow the eight wizard steps: **Basics**, **Cluster Add-ons**, **Node Pool**, **Log Storage**, **Monitoring**, **Grafana**, **Endpoints** and **Review & Submit**. See [Use](use.md).

Next: [Use](use.md).
