---
description: What you need before you start, how to activate Kubernetes Upgrader from the Agent Marketplace, and how to register your first cluster.
---

# Set Up

## Before you start

- An **AWS scope** in your workspace that points to the AWS account with your EKS clusters. Kubernetes Upgrader acts with that scope's IAM identity.
- An **IAM policy** on that identity that allows the AWS actions listed below.
- An **EKS access entry** for that identity on each cluster you want to upgrade, so Kubernetes Upgrader can cordon and drain nodes. `AmazonEKSClusterAdminPolicy` covers everything. See the least-privilege list below.
- A DuploCloud **Administrator** account. Only administrators can use Kubernetes Upgrader (see [Permissions and Safety](permissions-and-safety.md)).

{% hint style="info" %}
Missing read permissions only make a check show as "Unverified". Missing write permissions stop the step that needs them, with the AWS error.
{% endhint %}

<!-- VERIFY: Pre-flight checks need the Kubernetes API reachable from DuploCloud. A private-only endpoint makes plans finish with warnings or blockers. -->

### AWS permissions by feature

| Feature | AWS actions |
| --- | --- |
| Discover and register clusters | `eks:ListClusters`, `eks:DescribeCluster`, `eks:DescribeClusterVersions`, `ec2:DescribeRegions`, `sts:GetCallerIdentity` |
| Control plane upgrade | `eks:UpdateClusterVersion`, `eks:DescribeUpdate`, `eks:ListInsights` |
| Add-on upgrades | `eks:ListAddons`, `eks:DescribeAddon`, `eks:DescribeAddonVersions`, `eks:UpdateAddon` |
| Managed node groups | `eks:ListNodegroups`, `eks:DescribeNodegroup`, `eks:UpdateNodegroupVersion`, `eks:DescribeUpdate`; custom-AMI groups also `ec2:CreateLaunchTemplateVersion` |
| Self-managed worker swap | `autoscaling:DescribeAutoScalingGroups`, `autoscaling:DescribeScalingActivities`, `autoscaling:UpdateAutoScalingGroup`, `autoscaling:SetDesiredCapacity`, `autoscaling:CreateOrUpdateTags`, `autoscaling:DeleteTags`, `autoscaling:TerminateInstanceInAutoScalingGroup`, `ec2:DescribeInstances`, `ec2:DescribeImages`, `ec2:DescribeLaunchTemplateVersions`, `ec2:CreateLaunchTemplateVersion`, `ec2:ModifyLaunchTemplate` |
| Guard policy on the Duplo-Master role | `ec2:DescribeRegions`, `ec2:DescribeInstances`, `iam:GetInstanceProfile`, `iam:PutRolePolicy`, `iam:DeleteRolePolicy` |
| Image pre-flight check | `ecr:DescribeImages`, `ecr:DescribePullThroughCacheRules`, `ecr:GetAuthorizationToken`, `ecr:BatchGetImage` |
| EC2 capacity pre-flight check | `servicequotas:GetServiceQuota`, `servicequotas:GetAWSDefaultServiceQuota`, `ec2:DescribeInstances`, `ec2:DescribeInstanceTypes`, `ec2:DescribeSubnets` |

In AWS GovCloud use the `arn:aws-us-gov:` partition in resource ARNs.

<!-- VERIFY: source is the extension README "Required permissions". Confirm the list is current for the released version, and whether we publish a ready-made policy or CloudFormation template for customers. -->

### Kubernetes permissions

The same identity, mapped through an EKS access entry or `aws-auth`, needs `AmazonEKSClusterAdminPolicy`, or the least-privilege equivalent:

| Resource | Verbs | Used for |
| --- | --- | --- |
| `nodes` | get, list, patch | readiness check, cordon |
| `pods` | get, list, delete | drain and workload checks |
| `pods/eviction` | create | drain (honours PodDisruptionBudgets) |
| `deployments`, `statefulsets` | get, list, patch | rolling restart, pausing cluster-autoscaler |
| `replicasets` | get | find a pod's Deployment |
| `poddisruptionbudgets` | list | availability check |
| `persistentvolumeclaims`, `persistentvolumes` | get | EBS zone check |
| `serviceaccounts`, `secrets` | get | image pull secrets for the image check |
| `namespaces`, `events` and other reads | get, list | the read-only `kubectl` console and Ask AI |

## Activate Kubernetes Upgrader

1. Switch to **AI Admin**, open **Marketplace**, and select the **Agent Marketplace** tab.
2. Find **Kubernetes Upgrader**, select **Activate** and confirm.
3. When it finishes, it appears in the **AI Admin** menu as **Kubernetes Upgrader > Kubernetes Clusters**. It isn't added to a workspace's menu.

<!-- VERIFY: exact marketplace button names. Screenshots KU-01 and KU-02. -->

## Who can use it

Only administrators. There is nothing to grant: people without the Administrator role can't see or use Kubernetes Upgrader, whatever their permission sets say. See [Permissions and Safety](permissions-and-safety.md).

## Register your first cluster

1. In **AI Admin**, open **Kubernetes Upgrader > Kubernetes Clusters**.
2. In **Workspace** at the top of the list, choose the workspace whose AWS scope reaches the cluster. Kubernetes Upgrader remembers your choice.
3. Select **Add Kubernetes Cluster**.
4. Choose the **AWS scope** and the **region**.
5. Choose the cluster from the list. Kubernetes Upgrader discovers the clusters that scope can see.
6. Give the registration a unique label and save.

<!-- VERIFY: field names against the live form (screenshots KU-03, KU-04). -->

Next: [Use](use.md).
