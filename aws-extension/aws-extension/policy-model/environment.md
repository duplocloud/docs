---
description: >-
  A deployment boundary inside a cluster, isolating teams, applications, or
  stages from each other.
---

# Environment

An Environment is a deployment boundary inside a Cluster. It provides isolation between teams, applications, or stages (development, staging, production). On AWS, it provisions a dedicated set of resources: security groups, IAM roles, and KMS encryption keys.

All workloads, Kubernetes resources, and databases created inside an Environment inherit its access and network boundaries.

## Spec

| Field | Description |
|---|---|
| **Cluster** | The Cluster Baseline this Environment lives inside |
| **Plans** | AWS only. One or more Plans to associate with this Environment. Plans provide hosted zones, ACM certificates, and AMI references available to resources in the Environment |

## Result

On AWS, the Environment result includes:

| Field | Description |
|---|---|
| **Security Groups** | Dedicated security groups controlling inbound and outbound traffic for resources in this Environment |
| **IAM Roles** | IAM roles scoped to this Environment for workloads and service accounts |
| **KMS Keys** | Encryption keys for secrets and storage resources in this Environment |
| **Resource Groups** | A count of the sub-resources (Kubernetes resources, databases, etc.) provisioned inside the Environment |

## Navigation

The Environment detail view provides a full resource tree in the left navigation — covering Kubernetes resources (Namespaces, Workloads, Configs, Storage) and Cloud Resources (Databases, Hosts, Networks). Each sub-resource has its own list view, create form, and detail page.

## Dependencies

An Environment requires a **Cluster Baseline**.

{% hint style="warning" %}
An Environment cannot be deprovisioned while workloads or databases are running inside it. Deprovision all child resources first.
{% endhint %}

## What's next

With an Environment ready, you can create resources inside it:

* [Kubernetes Resources](kubernetes/README.md) — Namespaces, Workloads, Configs, and Storage
* [Databases](databases/README.md) — RDS and ElastiCache instances on AWS
