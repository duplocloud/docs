---
description: Kubernetes resources managed inside an Environment — namespaces, workloads, configs, secrets, and storage.
---

# Kubernetes Resources

Once an Environment is provisioned, you can create and manage Kubernetes resources inside it. These resources live within the Environment's EKS cluster and inherit its IAM and network boundaries.

## Resource Types

<table data-view="cards">
  <thead>
    <tr>
      <th>Title</th>
      <th>Description</th>
      <th data-card-target data-type="content-ref">Target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Namespaces</strong></td>
      <td>Logical partitions within the cluster for organizing and isolating workloads.</td>
      <td><a href="namespaces.md">Namespaces</a></td>
    </tr>
    <tr>
      <td><strong>Node Groups</strong></td>
      <td>EC2 node groups that provide compute capacity for the cluster.</td>
      <td><a href="node-groups.md">Node Groups</a></td>
    </tr>
    <tr>
      <td><strong>Workloads</strong></td>
      <td>Deployments, DaemonSets, StatefulSets, and CronJobs.</td>
      <td><a href="workloads.md">Workloads</a></td>
    </tr>
    <tr>
      <td><strong>Configs and Secrets</strong></td>
      <td>ConfigMaps and Kubernetes Secrets.</td>
      <td><a href="configs-and-secrets.md">Configs and Secrets</a></td>
    </tr>
    <tr>
      <td><strong>Storage</strong></td>
      <td>Persistent Volume Claims and Storage Classes.</td>
      <td><a href="storage.md">Storage</a></td>
    </tr>
  </tbody>
</table>

All Kubernetes resources are scoped to an **Environment**. To create any of these resources, an Environment must already be provisioned.
