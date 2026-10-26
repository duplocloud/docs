---
description: Persistent storage for Kubernetes workloads — Storage Classes and Persistent Volume Claims.
---

# Storage

**Storage Classes** define the type and properties of persistent storage available in the cluster — the provisioner, volume type (e.g. gp3, io1), reclaim policy, and binding mode.

**Persistent Volume Claims (PVCs)** are requests for storage by a workload. A PVC is bound to a Persistent Volume provisioned according to the Storage Class. StatefulSets and other workloads reference PVCs to attach durable storage to their pods.

## Storage Classes

| Field | Description |
|---|---|
| **Name** | The Storage Class name |
| **Volume Type** | The EBS volume type (e.g. `gp3`, `io1`) |
| **Reclaim Policy** | What happens to the volume when the PVC is deleted: `Delete` or `Retain` |
| **Binding Mode** | `Immediate` or `WaitForFirstConsumer` |
| **Encrypted** | Whether volumes are encrypted at rest |

## Persistent Volume Claims

| Field | Description |
|---|---|
| **Name** | The PVC name |
| **Namespace** | The Namespace this PVC belongs to |
| **Storage Class** | The Storage Class to provision from |
| **Access Mode** | `ReadWriteOnce`, `ReadOnlyMany`, or `ReadWriteMany` |
| **Storage Size** | Requested storage size (e.g. `20Gi`) |

## Dependencies

Storage Classes and PVCs require an **Environment**.
