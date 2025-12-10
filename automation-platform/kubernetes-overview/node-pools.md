---
description: Provisioning and Managing Kubernetes Node Pools in DuploCloud
---

# Node Pools

[Kubernetes Node Pools](https://kubernetes.io/docs/concepts/architecture/nodes/) are collections of worker nodes within a Kubernetes cluster that share the same configuration, such as instance type, number of nodes, availability zones, and special hardware features. They allow you to tailor compute resources to meet the needs of different workloads.

Node Pools simplify node management by grouping nodes with similar characteristics, enabling easier scaling, upgrades, and maintenance.

### Creating a Node Pool

1. In the DuploCloud Portal, navigate to **Kubernetes** → **Nodes**.
2.  Click **Add**. The **Add Node Pool** pane displays.<br>

    <figure><img src="../../.gitbook/assets/Screenshot (734).png" alt=""><figcaption><p><strong>Add Node Pool</strong> pane</p></figcaption></figure>
3. Complete the required fields:

<table data-header-hidden><thead><tr><th width="213.99993896484375"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the node pool. </td></tr><tr><td><strong>Expiration (In hours)</strong></td><td>Enter the number of hours after which the nodes in this pool should automatically expire and be deleted.</td></tr><tr><td><strong>Termination Grace Period (In hours)</strong></td><td>Enter the time allowed for the node to drain its pods before they are forcefully deleted and the node is removed. If you're using <strong>EKS Auto Mode</strong> and leave this field blank, it defaults to <strong>24 hours</strong>.</td></tr><tr><td><strong>CPU Limits</strong></td><td>Enter the total number of vCPUs to allocate to this node pool. This helps control scaling behavior.</td></tr><tr><td><strong>Memory Limits (In Gi)</strong></td><td>Enter the total memory (in GiB) to allocate to this node pool.</td></tr><tr><td><strong>Disruption Consolidation Policy</strong></td><td><p>Select to determine how EKS handles potential disruptions to running workloads when performing node consolidation:</p><ul><li><strong>When Empty</strong>: Nodes are only considered for disruption (removal or replacement) if they have no running pods.</li><li><strong>When Empty or Underutilized</strong>: Nodes are considered for disruption if they are empty or have been underutilized for the duration specified in the <strong>Consolidate After</strong> field</li></ul></td></tr><tr><td><strong>Consolidate After (In min)</strong></td><td>Enter the number of minutes to wait before consolidating nodes after a disruption is detected.</td></tr><tr><td><strong>Requirements</strong></td><td>Click the <strong>Add</strong> button and use <strong>Key</strong>, <strong>Operator</strong>, and <strong>Value</strong> to define node selection rules for workload placement. This allows you to target specific instance types, zones, or other node attributes.</td></tr></tbody></table>

4. Click **Create** to provision the Node Pool.

### Additional Resources

* [Creating an Infrastructure with EKS Auto Mode](../overview/use-cases/eks-auto-mode.md#creating-an-infrastructure-with-eks-auto-mode)
* [GKE Node Pools](../overview-1/gcp-services/node-pools.md)
