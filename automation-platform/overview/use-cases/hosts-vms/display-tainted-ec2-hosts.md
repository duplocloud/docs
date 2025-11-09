---
description: Manage taints for EKS nodes in the DuploCloud Portal
---

# Taints for EKS Nodes

Taints influence Kubernetes workload scheduling by marking nodes with specific conditions that certain Pods must tolerate to be scheduled on those nodes. Taints ensure that only compatible workloads run on a node, which can be useful for restricting access to certain resources, isolating environments, or managing resource usage.

Kubernetes can automatically add taints to nodes, for example, when a node becomes unreachable or has health issues, Kubernetes may apply a taint to prevent new workloads from being scheduled there. Certain workloads might require a specific configuration, so taints help ensure only compatible resources are used.

In addition to these automatic taints, you can control workload distribution by manually adding taints to EKS nodes or agent pools in the DuploCloud Portal.

## Adding Taints in the DuploCloud Portal

1. When [Adding a Host](adding-hosts.md) in the DuploCloud Portal, click the **Add Taint** button at the bottom right of the Advanced Options section. The **Add Taint** pane displays.
2. Complete the following fields:
   * **Key**: Identifies the taint condition, e.g., `dedicated`, or `testing`.
   * **Value**: Additional context for the key, such as `dev`, `staging`, or `prod`.
   * **Effect**: Specifies the action taken if a Pod does not tolerate the taint:
     * **No Schedule**: Prevents the Pod from being scheduled on the node unless it tolerates the taint.
     * **Prefer No Schedule**: Kubernetes will try to avoid scheduling the Pod on this node, but it may still schedule it if necessary.
     * **No Execute**: Immediately evicts existing Pods that don’t tolerate the taint and prevents new ones from being scheduled there.

<div align="left"><figure><img src="../../../../.gitbook/assets/Add taint.png" alt="" width="407"><figcaption><p>The Add Taint pane in the DuploCloud Portal</p></figcaption></figure></div>

3. Click **Add Taint**. The taint is added to the node.&#x20;

## Viewing Taints

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Hosts**.&#x20;
2. Navigate to the **EC2** or **ASG** tab, and check for Hosts with a status of **Stopped** and **Tainted**. The connection to the underlying node is lost if these statuses are present.&#x20;
3. Click on the **Tainted** status to display the taints.&#x20;

<figure><img src="../../../../.gitbook/assets/taint success (1).png" alt=""><figcaption></figcaption></figure>

See the [kubectl documentation](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#taint) for commands, flags, and examples to resolve taints.&#x20;
