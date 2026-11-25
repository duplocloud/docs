---
description: What Standard Observability can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

## What it can read and change

Standard Observability acts with the IAM role behind the stack's AWS scope and the Kubernetes identity behind its Kubernetes scope. It can only do what those identities allow.

| | What it does |
| --- | --- |
| **Reads** | The EKS cluster, its VPC, subnets, route tables, security group rules and instances. ACM certificates and EKS clusters, to fill the wizard's lists. The cluster's add-ons, StorageClasses and any existing Prometheus Operator. The state of its own Helm releases. |
| **Changes in AWS** | Creates an EKS node group and its IAM role, unless you use existing nodes. Adds security group rules, each allowing one source on one port. Creates an S3 gateway VPC endpoint, or adds route tables to an existing one. Creates the log bucket, encrypted with public access blocked, unless you supply one. Creates the cluster's IAM OIDC provider if missing, and an IAM role that only Loki's service account can use, limited to the log bucket. The template also creates a permissions boundary, `<RoleName>-irsa-boundary`, and that role can only be created under it, so it can never reach more than the log buckets. |
| **Changes in Kubernetes** | Creates the namespace if it doesn't exist. Applies Flux Helm repositories and releases for Loki, Grafana, the log collectors and Prometheus. Creates the `grafana-admin` Secret, the sign-in proxy, a NetworkPolicy so only the proxy reaches Grafana, a service account, and Ingresses. Through the Ingresses, the AWS Load Balancer Controller creates a public load balancer for Grafana and the optional internal ones. |
| **Changes in DuploCloud** | Creates the stack record and its ticket. Adds a workspace setting so your portal can sign people in to Grafana. Creates a Grafana provider and scope, and attaches the scope to the workspace. |
| **Never** | Edits or removes existing security group rules. Overwrites a Kubernetes object it didn't create. Changes or deletes anything you supplied (a bucket, node group, role, namespace or OIDC provider). Installs or turns off cluster add-ons. Deletes your log bucket or metric volume. |

{% hint style="warning" %}
Grafana's load balancer is **internet-facing**, and there is no internal-only option. Sign-in goes through your DuploCloud portal, and a NetworkPolicy stops other pods reaching Grafana directly. Choose the hostname and certificate with that in mind.
{% endhint %}

### AWS permissions

The CloudFormation template in [Set Up](set-up.md#create-the-iam-role) creates a role with exactly these permissions:

| Area | Actions | Used for |
| --- | --- | --- |
| Identity | `sts:GetCallerIdentity` | The check every run starts with |
| EKS | `ListClusters`, `DescribeCluster`, `DescribeNodegroup`, `CreateNodegroup`, `DeleteNodegroup`, `TagResource`, `AccessKubernetesApi` | The node pool, Kubernetes API access, and the wizard's cluster list |
| ACM | `ListCertificates` | The wizard's certificate list |
| EC2 | `DescribeSubnets`, `DescribeRouteTables`, `DescribeInstances`, `DescribeVpcEndpoints`, `DescribeSecurityGroupRules`, `CreateVpcEndpoint`, `ModifyVpcEndpoint`, `AuthorizeSecurityGroupIngress`, `CreateTags` | The S3 VPC endpoint and the security group rules. There is no delete or revoke permission, so teardown never removes either. |
| IAM | `GetRole`, `ListAttachedRolePolicies`, `ListRolePolicies`, `CreateRole`, `TagRole`, `DeleteRole`, `AttachRolePolicy` and `DetachRolePolicy` (only the three AWS EKS node policies), `PutRolePolicy`, `PutRolePermissionsBoundary`, `DeleteRolePolicy`, `UpdateAssumeRolePolicy`, `GetPolicy`, `ListOpenIDConnectProviders`, `CreateOpenIDConnectProvider`, and `PassRole` only for the node role and only to `eks.amazonaws.com` | The node role, the OIDC provider and the log-access role. The roles it can create are limited to names ending `-observability-node` and `-observability-s3`. |
| S3 | `ListBucket`, `CreateBucket`, `PutBucketPublicAccessBlock`, `PutEncryptionConfiguration` | Creating the log bucket |

Route 53 isn't in the list, because the agent doesn't create DNS records itself. If you choose **Create it automatically (external-dns)**, external-dns on the cluster creates the record with its own permissions.

### Kubernetes access

If you set **EksClusterName** in the template, the role gets **cluster-admin** on that cluster. For narrower access, apply the scoped RBAC manifest that ships with the agent (`standard-observability-rbac.yaml`) instead. It grants a namespaced role for the objects the stack manages, plus read-only cluster access for the add-on check.

## Who can do what

Stacks belong to a workspace, and DuploCloud permission sets decide who can see and change them. On top of that, Standard Observability checks every scope a request uses. The scope must be attached to the workspace, and a user who isn't an administrator must also be granted the scope by their permission sets.

| Capability | Read-only user | Regular user | Administrator |
| --- | :---: | :---: | :---: |
| See stacks, stack pages and dashboards | Yes | Yes | Yes |
| Create, edit or deprovision a stack | No | Yes, with scopes granted to them | Yes |
| Delete a stack record | No | Yes | Yes |
| Re-check the endpoint, change favourites | No | Yes | Yes |
| Use the setup page (default scopes, create scopes) | No | No | Yes |

"Read-only" and "regular" mean what your DuploCloud permission sets grant on stacks in the workspace. A regular user can only pick scopes attached to the workspace and granted to them. Other scopes are refused with "You cannot use the selected scope here".

## What needs confirmation

- **Creating a stack.** Nothing is created until you submit on the wizard's **Review & Submit** step.
- **Editing a stack.** Saving runs provisioning again, with no extra prompt.
- **Tearing down a stack.** DuploCloud shows what will be removed and kept, and asks you to confirm. Then the agent previews the teardown in the ticket and waits for you to confirm again in a new message. The teardown runs only if the plan still matches the preview you confirmed, so a stale preview can't be approved.

## Safety checks

- **Fails before creating anything** if the S3 VPC endpoint can't be set up. There is no fallback to the NAT gateway.
- **Fails before installing anything** if another active cluster-wide Prometheus Operator is in the cluster, or there's no usable StorageClass.
- **Never overwrites.** Before applying any Kubernetes object, the stack checks whether one with the same name exists and isn't its own. If so, it stops and names it.
- **Only removes what it created.** Teardown works from the stack's list of created resources, in reverse order. Anything you supplied isn't on that list.
- **Keeps your data.** Teardown keeps the log bucket and the Prometheus volume.
- **Keeps the admin password out of sight.** The password goes into the `grafana-admin` Kubernetes Secret, not chart values, and DuploCloud never shows it or returns it from the API. Reading it needs access to that Secret in the cluster.
- **One run at a time.** A second run on the same stack stops without changing anything.

## AI safety

The provisioning agent runs the agent's built-in script and reports the result. If the script fails, the agent reports the reason and stops. It doesn't make AWS or Kubernetes changes by hand, retry with workarounds, or widen permissions.

The agent treats everything it reads as data, never as instructions. That covers ticket messages, cluster output and file contents. If any of it asks the agent to run a command, skip a step or reveal a credential, the agent quotes it in the ticket and carries on as before. It never opens or prints the credential files or the Grafana password.

## Limits

- Failed runs aren't rolled back. Whatever was created stays until you fix the cause and run again (edit and save), or tear the stack down.
- Teardown keeps the log bucket, Prometheus volume, S3 VPC endpoint, security group rules, namespace and OIDC provider. Remove them yourself if you no longer need them.
- No Alertmanager. Alerts are visible in Prometheus and Grafana but aren't sent anywhere.
- The mode, cluster and namespace can't be changed after creation.
