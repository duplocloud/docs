---
description: >-
  The building blocks of the AWS Extension — resources, their specs, results,
  and how they relate to each other.
---

# AWS Extension Policy Model

The AWS Extension Policy Model defines the resources the extension manages and how they relate to each other. Understanding this model helps you understand what the extension can do and why the creation flow follows the order it does.

## The Resource Hierarchy

The AWS Extension organizes infrastructure as a hierarchy. Each level depends on the one above it:

**Network Baseline → Cluster Baseline → Environment → Workloads and Databases**

{% hint style="info" %}
Policy model diagram coming soon.
{% endhint %}

A **Network Baseline** establishes the VPC — the networking foundation everything else runs on. A **Cluster Baseline** provisions an EKS cluster inside that network. An **Environment** creates a deployment boundary inside a cluster, with its own security groups, IAM roles, and KMS keys. Workloads, databases, and other resources live inside environments.

**Plans** catalog AWS account-level resources — hosted zones, ACM certificates, and AMIs — that environments and workloads can reference.

**Faults** surface issues across any resource at any level of the hierarchy.

## Resource Lifecycle

Every resource in the AWS Extension follows the same status lifecycle. Each resource has a **Spec** tab showing what was requested, a **Result** tab showing what was provisioned, and a link to the underlying ticket that executed the work. Updates trigger a reconciliation — the agent handles only the delta, not a full teardown and rebuild.

<details>

<summary>View all lifecycle states</summary>

| Status | Description |
|---|---|
| **Pending** | Resource has been created and is waiting to be provisioned |
| **Provisioning** | The AI agent is actively provisioning the resource |
| **Ready** | Resource is live and available |
| **Failed** | Provisioning or an update encountered an error |
| **Blocked** | Waiting for user input before proceeding |
| **Awaiting Approval** | A change is pending approval before it is applied |
| **DeProvisioning** | Resource is being torn down |
| **DeProvisioned** | Resource has been removed |

</details>

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
      <td><strong>Network Baseline</strong></td>
      <td>VPC with subnets, routing, and NAT — the networking foundation.</td>
      <td><a href="network-baseline.md">Network Baseline</a></td>
    </tr>
    <tr>
      <td><strong>Cluster Baseline</strong></td>
      <td>EKS cluster built on top of a Network Baseline.</td>
      <td><a href="cluster-baseline.md">Cluster Baseline</a></td>
    </tr>
    <tr>
      <td><strong>Environment</strong></td>
      <td>Deployment boundary inside a cluster, with IAM and security group isolation.</td>
      <td><a href="environment.md">Environment</a></td>
    </tr>
    <tr>
      <td><strong>Plan</strong></td>
      <td>AWS account-level catalog: hosted zones, certificates, and AMIs.</td>
      <td><a href="plan.md">Plan</a></td>
    </tr>
    <tr>
      <td><strong>Faults</strong></td>
      <td>Cross-resource issues detected across the hierarchy.</td>
      <td><a href="faults.md">Faults</a></td>
    </tr>
    <tr>
      <td><strong>Kubernetes Resources</strong></td>
      <td>Namespaces, workloads, configs, secrets, and storage inside an Environment.</td>
      <td><a href="kubernetes/README.md">Kubernetes Resources</a></td>
    </tr>
    <tr>
      <td><strong>Databases</strong></td>
      <td>RDS and ElastiCache instances inside an Environment.</td>
      <td><a href="databases/README.md">Databases</a></td>
    </tr>
  </tbody>
</table>
