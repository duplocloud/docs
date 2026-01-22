---
description: Create Kubernetes Jobs in AWS and GCP from the DuploCloud Portal
---

# Jobs

In Kubernetes, a [Job ](https://kubernetes.io/docs/concepts/workloads/controllers/job/)is a controller object representing a task or a set of tasks that runs until successful completion. It is designed to manage short-lived batch workloads in a Kubernetes cluster. Use a Kubernetes Job when you need to run a task or a set of tasks once, to completion, rather than continuously, as in other types of controllers like [Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).

Refer to the Kubernetes [Job ](https://kubernetes.io/docs/concepts/workloads/controllers/job/)documentation for use cases and examples of when to use Kubernetes Jobs.

## Using Kubernetes Jobs for Pod management

In the DuploCloud Portal, you can create K8s Jobs to create one or more Pods. The Job retries until a specified number of Pods are successfully executed. Kubernetes Jobs tracks successful terminations, and when the specified number of successful terminations are completed, the Job is marked as completed in Kubernetes. Deleting a Kubernetes Job cleans up the Pods that it created. Suspending a Kubernetes Job deletes its active Pods until it is resumed.

You typically create one Kubernetes Job object to run one Pod to completion reliably. The Job object starts a new Pod if the first Pod fails or is deleted (for example, in case of a node hardware failure or a node reboot).

You can also use a Kubernetes Job to run multiple Pods in [parallel](https://kubernetes.io/docs/tasks/job/parallel-processing-expansion/). If you want to run a Kubernetes Job (a single task or several in parallel) on a schedule, see Kubernetes [CronJobs](cronjobs.md).

## Creating a Kubernetes Job

1. Navigate to **Kubernetes** -> **Job**.
2.  Click **Add**. The **Add Kubernetes Job** page displays.<br>

    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (969).png" alt=""><figcaption><p><strong>Add Kubernetes Job</strong> - <strong>Basic Options</strong> page</p></figcaption></figure></div>
3. Complete the fields as follows:

<table data-header-hidden><thead><tr><th width="274.22222900390625"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the Job, e.g., <code>job1</code>. Required.</td></tr><tr><td><strong>Cleanup After Finished in Seconds (TTL)</strong></td><td>Enter a TTL value in seconds, e.g., <code>86400</code>.</td></tr><tr><td><strong>Restart Policy</strong></td><td>Select the restart policy, e.g., <strong>Never</strong>.</td></tr><tr><td><strong>Backoff Limit</strong></td><td>Enter the maximum number of retries before the Job is marked failed.</td></tr><tr><td><strong>Allocation Tag</strong></td><td>Enter Allocation Tags if needed for resource allocation.</td></tr></tbody></table>

4. Enter the details for **Container 1** as needed (**Container Name**, **Docker Image**, **Command**, **Environment Variables**, **Arguments**, **Other Container Config**).
   * If your Job requires **Init Containers**, click the caret next to **Add Container** and select **Add Init Container**.
   * To add more containers, click **Add Container** as many times as needed and fill in their details.

<table data-header-hidden><thead><tr><th width="228"></th><th></th></tr></thead><tbody><tr><td><strong>Container Name</strong></td><td>Enter the container name, e.g., <code>main</code>. Required.</td></tr><tr><td><strong>Docker Image</strong></td><td>Enter the Docker image to run, e.g., <code>nginx:latest</code>. Required.</td></tr><tr><td><strong>Command</strong></td><td>Enter any commands to run in the container.</td></tr><tr><td><strong>Environment Variables</strong></td><td>Enter environment variables to set in the container.</td></tr><tr><td><strong>Arguments</strong></td><td>Enter arguments for the container.</td></tr><tr><td><strong>Other Container Config</strong></td><td>Enter any additional container configuration.</td></tr></tbody></table>

5. Click **Next**. The **Advanced Options** pane displays.

<div align="left"><figure><img src="../.gitbook/assets/Screenshot (970).png" alt=""><figcaption><p><strong>Add Kubernetes Job</strong> - <strong>Advanced Options</strong> pane</p></figcaption></figure></div>

6. Complete the additional fields as needed:

<table data-header-hidden><thead><tr><th width="229.77777099609375"></th><th></th></tr></thead><tbody><tr><td><strong>Other Spec Configuration</strong></td><td>Enter any additional container or pod specifications needed.</td></tr><tr><td><strong>Metadata Annotations</strong></td><td>Enter annotations in <code>key=value</code> format to add custom metadata to the Job or pods.</td></tr><tr><td><strong>Metadata Labels</strong></td><td>Enter labels in <code>key=value</code> format. To specify an App Name, use: <code>app.duplocloud.net/app-name: "&#x3C;your-app-name>"</code></td></tr></tbody></table>

7. Click **Create**. The job is created and displayed on the **Job** page with a status of **Active**.&#x20;

<figure><img src="../.gitbook/assets/complete pi.png" alt=""><figcaption><p><strong>K8s Job</strong> tab showin<strong>g</strong> the Active <strong>CALCULATEPI</strong> Job.</p></figcaption></figure>

{% hint style="info" %}
**Tip:** Entering an app name in **Metadata Labels** allows the Job to be grouped by app on the [Apps page](../automation-platform/kubernetes-overview/viewing-kubernetes-apps.md).
{% endhint %}

### Using Allocation Tags with Kubernetes Jobs

Allocation tags for Kubernetes Jobs (labels, node selectors, or node affinity) help manage resources in a Kubernetes environment. They can be useful for:&#x20;

* **Resource Organization**
* **Scheduling and Affinity Rules**
* **Resource Quotas and Limits**
* **Monitoring and Logging**
* **Cost Allocation and Billing**

You can add allocation tags in the Allocation Tag field when creating Kubernetes Jobs.&#x20;

In the YAML below, the following act as allocation tags:

* **`labels`** are key-value pairs used to organize, categorize, and identify resources such as Pods, Nodes, Jobs, and more. The `compliance: HIPAA` label applied in the example indicates that the Kubernetes Job is associated with a HIPAA compliance context.
* **`nodeSelector`** specifies that the Kubernetes Job should be scheduled on specific nodes. In this example, it will be scheduled on nodes with the label `security-level: high.`

```yaml
  labels:
    compliance: HIPAA
spec:
  template:
    spec:
      nodeSelector:
        security-level: high
```

To learn more about allocation tags for Kubernetes Jobs, see the Kubernetes documentation on [labels and selectors](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) and [node selectors and node affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector).

## Managing Kubernetes Jobs faults

You can manage/override Kubernetes Jobs faults on a Tenant or Job level. If a Job fails, and no Tenant- or Job-level fault setting is configured, DuploCloud will generate a fault by default.&#x20;

### **Tenant-level Kubernetes Jobs faults**

Enable or disable faults for failed Kubernetes Jobs in a specific Tenant.

1. From the DuploCloud Portal, navigate to **Administrator** -> **Tenant.**
2. Click the Tenant name in the **NAME** column.&#x20;
3. Select the **Settings** tab, and click **Add**. The **Add Tenant Feature** pane displays.&#x20;
4. From the **Select Feature** list box, select **Enable K8s job fault logging by default**, and use the toggle switch to enable or disable the setting.&#x20;
5.  Click **Add**. The Jobs fault setting is added. <br>

    <div align="left"><figure><img src="../.gitbook/assets/tenant faults feature.png" alt=""><figcaption><p>The <strong>Add Tenant Feature</strong> pane with <strong>Enable K8s Job fault logging by default</strong> enabled</p></figcaption></figure></div>

You can view the Jobs fault setting on the **Tenants** page (Navigate to **Administrator** -> **Tenant**, select the Tenant name) under the **Settings** tab. If the value is **true**, DuploCloud will generate a fault. If the value is **false**, DuploCloud will not generate a fault.&#x20;

<figure><img src="../.gitbook/assets/tenant setting set.png" alt=""><figcaption><p>The <strong>Tenant</strong> details page, <strong>Setting</strong>s tab, showing the configured Jobs fault setting</p></figcaption></figure>

### **Jobs-level Kubernetes Jobs faults**

You can configure the faults for a specific Job when creating the Job in DuploCloud. Fault settings added this way override Tenant-level settings. On the **Add Kubernetes Job** page, in the **Metadata Annotations** field, enter:&#x20;

`duplocloud.net/fault/when-failed: true.` or&#x20;

`duplocloud.net/fault/when-failed: false.`

When the value is true and the Job fails, DuploCloud will generate a fault. When the value is false and the Job fails, a fault will not be generated.&#x20;

## Viewing a Kubernetes Job&#x20;

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Job**.
2. Select the Kubernetes Job you want to view and click the **Overview**, **Containers**, and **Details** tabs for more information about the Job status and history.&#x20;

You can also view a Kubernetes Job's details by clicking the menu icon ( <img src="../.gitbook/assets/Kabab_three_Vertical_dots (1) (1).png" alt="" data-size="line"> ) icon to the left of the Job name and selecting **View**.

<figure><img src="../.gitbook/assets/screenshot-nimbusweb.me-2024.02.14-13_04_25.png" alt=""><figcaption><p><strong>Overview and Details</strong> tabs for a KubernetesJob<strong>.</strong></p></figcaption></figure>

<figure><img src="../.gitbook/assets/view.png" alt=""><figcaption><p>Job option menu with <strong>View</strong> option highlighted.</p></figcaption></figure>

### Using the Containers page to view linked Kubernetes Jobs

You can view K8s Jobs linked to Containers by clicking the Container **Name** on the **Containers** page (**Kubernetes** -> **Containers**).&#x20;

<figure><img src="../.gitbook/assets/screenshot-nimbusweb.me-2024.02.14-13_26_18.png" alt=""><figcaption><p>Clicking the Container <strong>Name</strong> on the <strong>Containers</strong> page to view a linked K8s job</p></figcaption></figure>

You can filter container names by using the search field at the top of the page, as in this example:

<figure><img src="../.gitbook/assets/screenshot-nimbusweb.me-2024.02.14-13_29_20.png" alt=""><figcaption><p>Highlighted search field on the <strong>Containers</strong> page.</p></figcaption></figure>

## Editing a Kubernetes Job

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Job**.
2. Select the K8s Job you want to edit.&#x20;
3. Click the options menu ( <img src="../.gitbook/assets/Kabab_three_Vertical_dots (1) (1).png" alt="" data-size="line"> ) icon to the left of the K8s Job you want to edit and select **Edit**.

You can edit and modify the following fields in the DuploCloud portal:

* **Cleanup After Finished in Seconds**
* **Other Spec Configuration**
* **Metadata Annotations**
* **Labels**

<figure><img src="../.gitbook/assets/edit.png" alt=""><figcaption><p><strong>Job</strong> page options menu with <strong>Edit</strong> option highlighted.</p></figcaption></figure>

## Deleting a Kubernetes Job

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Job**.
2. Select the K8s Job you want to delete.&#x20;
3. Click the Job options menu ( <img src="../.gitbook/assets/Kabab_three_Vertical_dots (1) (1).png" alt="" data-size="line"> ) icon to the left of the Job name and select **Delete**.

<figure><img src="../.gitbook/assets/delete.png" alt=""><figcaption><p>Job options menu with <strong>Delete</strong> option highlighted</p></figcaption></figure>

## Running Jobs on Shared Hosts

DuploCloud supports running Kubernetes Jobs on Shared Hosts in both AWS and Azure.&#x20;

For detailed steps, see the [Shared Hosts documentation for AWS](../automation-platform/overview/use-cases/hosts-vms/adding-shared-hosts.md) and [Shared Hosts documentation for Azure](../automation-platform/overview-2/use-cases/hosts-vms/shared-hosts.md).
