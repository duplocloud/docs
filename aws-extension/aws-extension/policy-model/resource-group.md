---
description: The isolation boundary that holds Kubernetes and cloud resources.
---

# Resource Group

A Resource Group is the isolation boundary of the Infrastructure Agent. Every resource created inside it inherits its boundaries. What it creates depends on the cloud:

| Cloud | What the Resource Group creates |
| --- | --- |
| **AWS** | An IAM role and policies (including the account-wide `duplo-rg-common` policy), security groups, a KMS key, and an EC2 key pair |
| **Azure** | An Azure resource group, plus a managed identity that the group's resources use to deploy into it and to read and write Key Vault secrets |
| **Oracle Cloud (OCI)** | A compartment. Access is granted by your tenancy's IAM policies, so no identity is created |

A Resource Group holds two kinds of children:

* **Kubernetes resources** — namespaces, workloads, jobs and cron jobs, ingress, config maps, secrets, storage, and Helm releases
* **Cloud resources** — on AWS: S3 buckets, RDS instances and clusters, ElastiCache, SNS topics, SQS queues, Lambda functions, Secrets Manager secrets, SSM parameters, EFS, MSK, ECR, and EC2 hosts. On Azure: Key Vaults, PostgreSQL flexible servers, Managed Redis, storage accounts, and virtual machines

## Spec

| Field | Description |
|---|---|
| **Name** | The name of the resource group |
| **Environment** | The Environment this group belongs to |
| **Cluster** | The Cluster Baseline whose cluster the group's Kubernetes resources run on |
| **Region** | The cloud region |
| **Tags** | Optional. User-defined tags inherited by every resource in the group |

## Tags

Tags set on a Resource Group are inherited by every resource inside it — applied as cloud tags (for example, **AWS tags**) on cloud resources and as **Kubernetes labels** on Kubernetes resources. Because a tag has to be valid in both systems, keys and values must satisfy the stricter of the two rule sets:

* A key may optionally carry a prefix, written `prefix/name`
* Key names, prefixes, and values must be valid Kubernetes label segments
* The `duplocloud.ai/` prefix is reserved and cannot be used
* A resource group can carry at most **50** tags

The platform stamps its own mandatory `duplocloud-ai-*` tags — workspace, environment, resource type, and managed-by — on top of whatever you set. Those are added automatically and don't count against your own tagging scheme.

{% hint style="info" %}
On Azure resource groups there is a second, separate tag list that applies only to the Azure resource group object itself, not to the resources inside it. The **Tags** field described here is the cloud-agnostic one that propagates to children.
{% endhint %}

## Deprovisioning

Deleting a Resource Group removes every resource inside it, so the platform requires an explicit confirmation of the whole contents rather than a single click.

Requesting deprovision first returns a **preview** listing every direct child that would be destroyed. You then confirm that list in full — the request is rejected if it omits any child that the preview returned. There is no partial deprovision: a Resource Group comes down with all of its children or not at all.

Individual resources have their own safeguards:

* **Delete** has been removed from resource views in favour of **Deprovision**, which tears down the cloud resource rather than just dropping the platform's record of it
* **Deprovision** and **Delete** are both disabled while delete protection is enabled on a resource
* Deprovisioning an imported network asks for confirmation first, since the network may have existed before the platform adopted it

## Dependencies

A Resource Group requires an **Environment**. Its Kubernetes resources additionally require the Environment's **Cluster Baseline**.
