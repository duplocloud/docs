---
description: EC2 node groups that provide compute capacity for your EKS cluster.
---

# Node Groups

Node Groups are managed groups of EC2 instances that provide compute capacity for the EKS cluster. Each node group defines the instance type, scaling configuration, and optional taints or labels applied to its nodes.

{% hint style="info" %}
If your Cluster Baseline uses **EKS Auto Mode**, AWS manages compute capacity automatically and node groups are not required.
{% endhint %}

## Spec

| Field | Description |
|---|---|
| **Name** | The name of the node group |
| **Instance Type** | The EC2 instance type for the nodes (e.g. `m5.large`) |
| **Minimum Nodes** | Minimum number of nodes in the group |
| **Desired Nodes** | Target number of nodes |
| **Maximum Nodes** | Maximum number of nodes (for autoscaling) |
| **Disk Size** | Root volume size in GB |
| **Taints** | Optional Kubernetes taints applied to all nodes in this group |
| **Labels** | Optional Kubernetes labels applied to all nodes in this group |

## Dependencies

Node Groups require a **Cluster Baseline**.
