---
description: >-
  Schedule a Kubernetes Job in AWS and GCP by creating a Kubernetes CronJob in
  the DuploCloud Portal
---

# CronJobs

A [Kubernetes ](https://kubernetes.io/)CronJob is a variant of a [Kubernetes Job](jobs.md) scheduled to run at periodic intervals.

See the Kubernetes [CronJob documentation](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/) for more information.

## Creating a Kubernetes CronJob

1. In the DuploCloud Portal, navigate to **Kubernetes** → **CronJob**.
2. Click **Add**. The **Add Kubernetes CronJob** page displays.
3. Navigate to **Kubernetes** → **CronJob**.
4.  Click **Add**. The **Add Kubernetes CronJob** page displays.<br>

    <figure><img src="../.gitbook/assets/cron 1.png" alt=""><figcaption><p><strong>Add Kubernetes CronJob</strong> - <strong>Basic Options</strong> page</p></figcaption></figure>
5.  Complete the fields as follows:

    <table data-header-hidden><thead><tr><th width="230.888916015625"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter the CronJob name, e.g., <code>cronjob1</code>. Required.</td></tr><tr><td><strong>Schedule</strong></td><td>Enter the Cron schedule in standard format, e.g., <code>0 2 * * *</code>. Required.</td></tr><tr><td><strong>Cleanup After Finished in Seconds (TTL)</strong></td><td>Enter TTL in seconds, e.g., <code>86400</code>.</td></tr><tr><td><strong>Restart Policy</strong></td><td>Select the restart policy, e.g., <strong>Never</strong>.</td></tr><tr><td><strong>Backoff Limit</strong></td><td>Enter the maximum number of retries before the Job is marked failed.</td></tr><tr><td><strong>Allocation Tag</strong></td><td>Enter allocation tags if needed for resource organization or scheduling.</td></tr></tbody></table>


6. Enter the details for **Container 1** as needed (**Container Name**, **Docker Image**, **Command**, **Environment Variables**, **Arguments**, **Other Container Config**).
   * If your CronJob requires **Init Containers**, click the caret next to **Add Container** and select **Add Init Container**. The **Init Container - 1** area displays.
   * To add more containers, click **Add Container** as many times as needed and fill in their details.

| **Container Name**         | Enter the container name, e.g., `main`. Required.       |
| -------------------------- | ------------------------------------------------------- |
| **Docker Image**           | Enter the Docker image, e.g., `nginx:latest`. Required. |
| **Command**                | Enter any commands to run in the container.             |
| **Environment Variables**  | Enter environment variables to set in the container.    |
| **Arguments**              | Enter arguments for the container.                      |
| **Other Container Config** | Enter any additional container configuration.           |

7. Click **Next**. The **Advanced Options** pane displays.&#x20;

<figure><img src="../.gitbook/assets/cron7.png" alt=""><figcaption><p><strong>Add Kubernetes CronJob</strong> - <strong>Advanced Options</strong> pane</p></figcaption></figure>

8. Complete the additional fields as needed:

<table data-header-hidden><thead><tr><th width="260"></th><th></th></tr></thead><tbody><tr><td><strong>Other Spec Configuration</strong></td><td>Enter any additional pod or container specifications as needed.</td></tr><tr><td><strong>Metadata Annotations</strong></td><td>Enter annotations in <code>key=value</code> format to add custom metadata to the CronJob or pods.</td></tr><tr><td><strong>Metadata Labels</strong></td><td>Enter labels in <code>key=value</code> format. To specify the App Name, use: <code>app.duplocloud.net/app-name: "&#x3C;your-app-name>"</code></td></tr></tbody></table>

8. Click **Create**. The Kubernetes CronJob is created and displayed on the **CronJob** page. It will run according to the schedule you specified.&#x20;

<figure><img src="../.gitbook/assets/Screenshot (916).png" alt=""><figcaption><p><strong>K8s CronJob</strong> tab displaying Kubernetes Job <strong>CALCULATEPI.</strong></p></figcaption></figure>

{% hint style="info" %}
**Tip:** Entering an app name in **Metadata Labels** allows the CronJob to be grouped under the specified App Name in the [Apps Dashboard](../automation-platform/kubernetes-overview/viewing-kubernetes-apps.md).
{% endhint %}

## Suspending a CronJob

DuploCloud lets you temporarily suspend a CronJob, pausing the scheduling of new Jobs while allowing any existing Jobs to continue running. By default, the suspend setting is `false` and CronJob will continue scheduling new Jobs.

To update the suspend setting:

1. Navigate to **Kubernetes** → **CronJobs**.
2. Click the menu icon (<img src="../.gitbook/assets/menu icon.avif" alt="" data-size="line">) for the CronJob you want to suspend.&#x20;
3. In the **Other Spec Configuration** field, locate the `suspend` property.
4.  Set the `suspend` value to `true` to suspend the CronJob or  `false` to resume scheduling.<br>

    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (915) (1).png" alt=""><figcaption></figcaption></figure></div>
5. The CronJobs page displays the current state in the **Suspended** column as **Yes** or **No**.

<figure><img src="../.gitbook/assets/Screenshot (918).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note:** Suspending a CronJob only prevents new Jobs from being scheduled. Any Jobs that were already created continue running until completion.
{% endhint %}

## Managing Kubernetes CronJobs faults

You can manage/override Kubernetes Jobs faults on a Tenant or CronJob level. If a CronJob fails, and no Tenant- or Job-level fault setting is configured, DuploCloud will generate a fault by default.&#x20;

### **Tenant-level Kubernetes CronJobs faults**

Enable or disable faults for failed Kubernetes CronJobs in a specific Tenant.

1. From the DuploCloud Portal, navigate to **Administrator** -> **Tenant.**
2. Click the Tenant name in the **NAME** column.&#x20;
3. Select the **Settings** tab, and click **Add**. The **Add Tenant Feature** pane displays.&#x20;
4. From the **Select Feature** list box, select **Enable K8s job fault logging by default**, and use the toggle switch to enable or disable the setting.&#x20;
5.  Click **Add**. The CronJobs fault setting is added. <br>

    <div align="left"><figure><img src="../.gitbook/assets/tenant faults feature.png" alt=""><figcaption><p>The <strong>Add Tenant Feature</strong> pane with <strong>Enable K8s Job fault logging by default</strong> enabled</p></figcaption></figure></div>

You can view the CronJobs fault setting on the **Tenants** page (Navigate to **Administrator** -> **Tenant**, select the Tenant name) under the **Settings** tab. If the value is **true**, DuploCloud will generate a fault. If the value is **false**, DuploCloud will not generate a fault.&#x20;

<figure><img src="../.gitbook/assets/tenant setting set.png" alt=""><figcaption><p>The <strong>Tenant</strong> details page, <strong>Setting</strong>s tab, showing the configured Jobs fault setting</p></figcaption></figure>

### **Jobs-level Kubernetes CronJobs faults**

You can configure the faults for a specific CronJob when creating the CronJob in DuploCloud. Fault settings added this way override Tenant-level settings. On the **Add Kubernetes Job** page, in the **Metadata Annotations** field, enter:&#x20;

`duplocloud.net/fault/when-failed: true.` or&#x20;

`duplocloud.net/fault/when-failed: false.`

When the value is true and the CronJob fails, DuploCloud will generate a fault. When the value is false and the CronJob fails, a fault will not be generated.&#x20;

## Viewing Kubernetes CronJobs

### Viewing CronJob Details&#x20;

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **CronJobs**.
2. Select the Kubernetes CronJob you want to view from the **NAME** colunm.
3. Select the **Overview, Schedule**, and **Details** tabs for information about the CronJob schedule and history.&#x20;

### Using the Containers page to view linked Kubernetes CronJobs

### **Viewing the Latest Job from a CronJob**

You can inspect the most recent CronJob execution from the link on the CronJob details page. This allows you to view the latest Job, including its logs, status, and container details, without manually browsing the Jobs list.&#x20;

1. Navigate to **Kubernetes** -> **CronJobs**.
2. Select the CronJob you want to inspect from the **NAME** column.&#x20;
3. Click the **Latest Scheduled Job** link in the heading. The Job details page displays, showing information about the most recent execution of the CronJob.

<figure><img src="../.gitbook/assets/cron link.png" alt=""><figcaption><p>The CronJob details page with the <strong>Latest Scheduled Job</strong> link highlighted</p></figcaption></figure>

<figure><img src="../.gitbook/assets/cron link dest.png" alt=""><figcaption><p>The Job details page displays page for the most recent execution of the CronJob.</p></figcaption></figure>

This enhancement improves traceability and simplifies debugging by reducing the steps needed to find and review recent executions.

### Viewing Kubernetes CronJobs by container

You can view the Kubernetes CronJobs associated with a specific container by following these steps:

1. In the DuploCloud Portal, navigate to **Kubernetes -> Containers**.
2. Select the container from the **NAME** column. You can filter container names using the **Search** field at the top of the page to narrow down your selection. The linked CronJob for that container displays, showing you the details of the job using it.

<figure><img src="../.gitbook/assets/Screenshot (393).png" alt=""><figcaption><p>The Job page for the CronJob associated with the selected container</p></figcaption></figure>

## Managing Kubernetes CronJobs

You can view, edit, delete, or manually run a Kubernetes CronJob from the options menu on the CronJobs page.

## Running CronJobs on Shared Hosts

DuploCloud supports running Kubernetes CronJobs on Shared Hosts in both AWS and Azure.&#x20;

For detailed steps, see the [Shared Hosts documentation for AWS](../automation-platform/overview/use-cases/hosts-vms/adding-shared-hosts.md) and [Shared Hosts documentation for Azure](../automation-platform/overview-2/use-cases/hosts-vms/shared-hosts.md).
