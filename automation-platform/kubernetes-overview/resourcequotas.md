---
description: Manage Kubernetes ResourceQuotas for DuploCloud Tenants
---

# ResourceQuotas

In DuploCloud, [Kubernetes ResourceQuotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/) control the total CPU, memory, and other resource usage allowed for workloads within each Tenant’s Kubernetes namespace, preventing Tenants from exceeding their resource allocations. You can create, view, update, and delete ResourceQuotas directly from the DuploCloud Portal.

## Adding a ResourceQuota

Create a new Kubernetes ResourceQuota limiting the total CPU, memory, or other resource usage allowed for workloads within your Tenant’s Kubernetes namespace.

1. In the DuploCloud Portal, navigate to **Administrator** → **Tenants**.
2. Select a Kubernetes-enabled Tenant from the **NAME** column.
3. Select the **Kubernetes Quota** tab.
4. Click Add. The **Add Resource Quota** pane displays.

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot (537).png" alt="" width="492"><figcaption><p><strong>Add Resource Quota</strong> pane</p></figcaption></figure></div>

5. Complete the fields shown in the table below.
   * &#x20;**Note**: You must enter a **Resource Quota Name** and specify **at least one resource constraint** (e.g., CPU, memory, or a custom quota key) to create a valid quota.

<table data-header-hidden><thead><tr><th width="302"></th><th></th></tr></thead><tbody><tr><td><strong>Resource Quota Name</strong></td><td>Enter a unique name for the ResourceQuota.</td></tr><tr><td><strong>Memory Request</strong></td><td>Specify the max total memory workloads can request (e.g., <strong>4Gi</strong>).</td></tr><tr><td><strong>Memory Limit</strong></td><td>Specify the max total memory workloads can use (e.g., <strong>8Gi</strong>).</td></tr><tr><td><strong>CPU Request</strong></td><td>Specify the max total CPU workloads can request.</td></tr><tr><td><strong>CPU Limit</strong></td><td>Specify the max total CPU workloads can use.</td></tr><tr><td><strong>Additional Resource Quota</strong></td><td>Enter YAML input for other quota keys (e.g., <code>count/pods: 100</code>).</td></tr><tr><td><strong>Scope Selector</strong></td><td>Enter YAML input to define a <code>scopeSelector</code> for quota enforcement.</td></tr></tbody></table>

3. Click **Add** to save the quota. DuploCloud creates a Kubernetes ResourceQuota in the Tenant's namespace.

## Managing ResourceQuotas

You can view, modify, or delete ResourceQuota for a Tenant from within the DuploCloud Portal.

1. In the DuploCloud Portal, navigate to **Administrator** → **Tenants**.
2. Select the Tenant you want to manage from the **NAME** column.
3. Select the **Resource Quota** tab.
4. Click the menu icon (<img src="../../.gitbook/assets/menu icon (13).avif" alt="" data-size="line">) at the end of the ResourceQuota’s row.
5. Choose one of the following actions:

<table data-header-hidden><thead><tr><th width="146.4444580078125">Action</th><th>Description</th></tr></thead><tbody><tr><td><strong>JSON</strong></td><td>View the ResourceQuota as a JSON representation.</td></tr><tr><td><strong>Edit</strong></td><td>Open the <strong>Update Resource Quota</strong> pane to modify fields.</td></tr><tr><td><strong>Delete</strong></td><td>Permanently remove the ResourceQuota.</td></tr></tbody></table>

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot (539).png" alt="" width="488"><figcaption><p> JSON representation of the <strong>basic-quota</strong> ResourceQuota</p></figcaption></figure></div>

## Additional Resources

* [Kubernetes: ResourceQuotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/)
