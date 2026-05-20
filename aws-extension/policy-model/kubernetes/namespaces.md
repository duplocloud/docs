---
description: Logical partitions within the cluster for organizing and isolating workloads.
---

# Namespaces

A Namespace is a Kubernetes construct that provides a logical partition within a cluster. Namespaces are used to organize workloads, apply resource quotas, and separate teams or applications within the same cluster.

## Spec

| Field | Description |
|---|---|
| **Name** | The name of the Namespace |
| **Environment** | The Environment this Namespace lives inside |

## Result

Once created, the Namespace is registered in the EKS cluster as a Kubernetes Namespace. Resources created inside it inherit the Environment's IAM roles and security group boundaries.

## Dependencies

A Namespace requires an **Environment**. Workloads, ConfigMaps, Secrets, and PVCs are created inside Namespaces.
