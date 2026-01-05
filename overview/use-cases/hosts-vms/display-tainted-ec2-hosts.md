---
description: Manage taints for EKS nodes in the DuploCloud Portal
---

# Taints for EKS Nodes

Taints influence Kubernetes workload scheduling by marking nodes with specific conditions that certain Pods must tolerate to be scheduled on those nodes. Taints ensure that only compatible workloads run on a node, which can be useful for restricting access to certain resources, isolating environments, or managing resource usage.

Kubernetes can automatically add taints to nodes, for example, when a node becomes unreachable or has health issues, Kubernetes may apply a taint to prevent new workloads from being scheduled there. Certain workloads might require a specific configuration, so taints help ensure only compatible resources are used.

In addition to these automatic taints, you can control workload distribution by manually adding taints to EKS nodes or agent pools in the DuploCloud Portal.

## Managing Taints on EKS Nodes

In DuploCloud, you can assign Kubernetes taints to EKS worker nodes to control how workloads are scheduled. Taints can be added during node creation or managed later from the node's detail page.

### Adding Taints During Node Creation

1.  When [Adding a Host](../../../automation-platform/overview/use-cases/hosts-vms/adding-hosts.md) in the DuploCloud Portal, click the **Add Taint** button at the bottom right of the Advanced Options section. The **Add Taint** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Add taint.png" alt="" width="407"><figcaption><p>The Add Taint pane in the DuploCloud Portal</p></figcaption></figure></div>
2. Complete the following fields:

<table data-header-hidden><thead><tr><th width="139.3333740234375"></th><th></th></tr></thead><tbody><tr><td><strong>Key</strong></td><td>Identify the taint condition. Example values: <code>dedicated</code>, <code>testing</code>.</td></tr><tr><td><strong>Value</strong></td><td>Provide additional context for the key. Example values: <code>dev</code>, <code>staging</code>, <code>prod</code>.</td></tr><tr><td><strong>Effect</strong></td><td>Specify the action taken if a Pod does not tolerate the taint:<br><br>• <strong>NoSchedule</strong>: Prevents the Pod from being scheduled on the node unless it tolerates the taint.<br>• <strong>PreferNoSchedule</strong>: Kubernetes avoids scheduling the Pod on this node if possible, but may still allow it.<br>• <strong>NoExecute</strong>: Immediately evicts existing Pods that don’t tolerate the taint and blocks new ones.</td></tr></tbody></table>

3. Click **Add Taint**. The taint is added to the node.&#x20;

### Adding Taints After Node Creation

To add a taint to an existing node:

1. Navigate to **Kubernetes** -> **Nodes**
2. Select the correct tab (**EC2**, **ASG**, etc.).
3. Click the **Name** of the node to open its details page.
4. Select the **Taints** tab.
5. Click **Add**. The **Add Taint** pane displays.&#x20;
6. Enter the **Key**, **Value**, and **Effect**.
7. Click **Add Taint.** The new taint will appear in the list immediately.

## Viewing Taints

You can view the taints applied to a node from the **Status** column in the **Nodes** list, or from the **Taints** tab on the **Node** details page.

### Viewing Taints from the Node List

1. Navigate to **Kubernetes** -> **Nodes**.
2. Look for the **Tainted** status under the **Status** column.
3. Click on the **Tainted** status for any node to open a list of taints applied to that node.

<figure><img src="../../../.gitbook/assets/taint success (1).png" alt=""><figcaption></figcaption></figure>

### Viewing Taints from the Node Details Page

1. Navigate to **Kubernetes** -> **Nodes**.
2. Click on the node in the **NAME** column.
3. Select the **Taints** tab. The **Taints** tab displays the key, value, and effect of each taint applied to the node.

{% hint style="info" %}
If you're familiar with `kubectl`, you can also manage taints from the command line. See the [official `kubectl taint` command reference](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#taint) for syntax and usage examples.
{% endhint %}

## Editing or Deleting Taints

1. Navigate to **Kubernetes** -> **Nodes**.
2. Click on the node in the **NAME** column.
3. Select the **Taints** tab.&#x20;
4. Click the menu icon (<img src="../../../.gitbook/assets/menu icon (29).avif" alt="" data-size="line">) next to the taint you want to manage.
5. Select **Edit** to modify the taint **Key**, **Value**, or **Effect** of the taint or **Delete** to remove the taint from the node.&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot (415).png" alt=""><figcaption><p>The <strong>Taints</strong> tab on the EC2 node details page</p></figcaption></figure>
