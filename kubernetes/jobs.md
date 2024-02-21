---
description: Create Kubernetes Jobs in AWS and GCP from the DuploCloud Portal
---

# Jobs

In Kubernetes, a [Job ](https://kubernetes.io/docs/concepts/workloads/controllers/job/)is a controller object that represents a task or a set of tasks that runs until successful completion. It is designed to manage short-lived, batch workloads in a Kubernetes cluster. You use a Job when you need to run a task or a set of tasks once, to completion, rather than continuously, as in other types of controllers such as [Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).

Refer to the Kubernetes [Job ](https://kubernetes.io/docs/concepts/workloads/controllers/job/)documentation for use cases and examples of when to use jobs.

## Using Kubernetes Jobs for Pod management

Pods are the smallest deployable units of computing that you can create and manage in Kubernetes. A Pod is a group of one or more [containers](https://kubernetes.io/docs/concepts/containers/), with shared storage and network resources, including a specification that dictates how to run the containers. A Pod's contents are always co-located and co-scheduled, and run in a shared context. A Pod models an application-specific "logical host": it contains one or more application containers that are tightly coupled.&#x20;

In the DuploCloud Portal, you can create K8s Jobs to create one or more Pods. The Job continues to retry execution of the Pods until a specified number of them successfully terminate. The K8s Jobs tracks the successful terminations. When the specified number of successful terminations completes, the Job is marked as `completed` in Kubernetes. Deleting a Job cleans up the Pods that the job created. Suspending a Job delete the Job's active Pods until the Job is resumed again.

You typically create one Job object to reliably run one Pod to completion. The Job object starts a new Pod if the first Pod fails or is deleted (for example, in case of a node hardware failure or a node reboot).

You can also use a Job to run multiple Pods in [parallel](https://kubernetes.io/docs/tasks/job/parallel-processing-expansion/). If you want to run a Job (either a single task, or several in parallel) on a schedule, see [CronJobs](cronjobs.md).

## Creating a Kubernetes Job in the DuploCloud portal

1. In the DuploCloud Portal, select the Tenant you are working with from the Tenant list box at the top-left of the DuploCloud Portal.&#x20;
2. Navigate to **Kubernetes** -> **Job**.
3. Click **Add**. The **Add Kubernetes Job** page displays.
4. In the **Basic Options** step, specify the Kubernetes Job **Name**.
5.  In the **Container - 1** area, specify the **Container Name** and associated **Docker Image**.\


    <figure><img src="../.gitbook/assets/screenshot-nimbusweb.me-2024.02.13-21_30_16.png" alt=""><figcaption><p><strong>Add Kubernetes Job</strong> page.</p></figcaption></figure>
6.  In the **Command** field, specify the command attributes for **Container - 1**. Click the Info Tip icon for examples. Select and **Copy** commands as needed.\


    <figure><img src="../.gitbook/assets/screenshot-nimbusweb.me-2024.02.13-21_36_00.png" alt=""><figcaption><p>The <strong>Add Kubernetes Job</strong> page with the <strong>Command</strong> info window.<br></p></figcaption></figure>

    <figure><img src="../.gitbook/assets/screenshot-nimbusweb.me-2024.02.13-21_37_24.png" alt=""><figcaption><p>Completed <strong>Command</strong> field for <strong>Container - 1.</strong></p></figcaption></figure>
7. To run the Job to completion, you must specify a Kubernetes [Init Container](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/).  Click the **Add Container** <img src="../.gitbook/assets/chevron_Down_arrow.png" alt="" data-size="line">button and select the **Add Init Container** option. The **Init Container - 1** area displays.
8.  In the **Init Container - 1** area, specify the **Container Name** and associated **Docker Image**.\


    <figure><img src="../.gitbook/assets/init job.png" alt=""><figcaption><p><strong>Add Init Container</strong> option on <strong>Add Container</strong> button in <strong>Container - 1</strong> area.</p></figcaption></figure>
9. Click **Next** to open the **Advanced Configuration** step.
10. In the **Other Spec Configuration** field, specify the Job spec (in YAML) for **Init Container - 1**. Click the Info Tip icon for examples. Select and **Copy** commands as needed.\


    <figure><img src="../.gitbook/assets/screenshot-nimbusweb.me-2024.02.14-12_41_36.png" alt=""><figcaption><p>Info Tip examples for <strong>Other Spec Configuration</strong> field in <strong>Advanced Configuration</strong> step for <strong>Init Container - 1.</strong><br></p></figcaption></figure>

    <figure><img src="../.gitbook/assets/screenshot-nimbusweb.me-2024.02.14-12_55_12.png" alt=""><figcaption><p>Completed <strong>Other Spec Configuration</strong> field for <strong>Init Container - 1.</strong> </p></figcaption></figure>
11. Click **Create**. The job is created and displayed on the **Job** page with a status of **Active**. \


    <figure><img src="../.gitbook/assets/screenshot-nimbusweb.me-2024.02.14-13_02_21.png" alt=""><figcaption><p><strong>K8S Job</strong> tab displaying Kubernetes job <strong>MY-K8S-INVOICE-JOB</strong> with <strong>Active Status.</strong></p></figcaption></figure>

## Viewing a Kubernetes Job&#x20;

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Job**.
2. Select the job you want to view and click the **Overview**, **Containers**, and **Details** tabs for more information about the job status and job history.&#x20;

You can also view details of a job by clicking the menu icon ( <img src="../.gitbook/assets/Kabab_three_Vertical_dots (5).png" alt="" data-size="line"> ) icon to the left of the job name and selecting **View**.

<figure><img src="../.gitbook/assets/screenshot-nimbusweb.me-2024.02.14-13_04_25.png" alt=""><figcaption><p><strong>Overview and Details</strong> tabs for Kubernetes job <strong>MY-K8S-INVOICE-JOB.</strong></p></figcaption></figure>

<figure><img src="../.gitbook/assets/view.png" alt=""><figcaption><p>Job option menu with <strong>View</strong> option highlighted.</p></figcaption></figure>

### Using the Containers page to view linked Kubernetes jobs

You can view K8s Jobs linked to Containers by clicking the Container **Name** on the **Containers** page (**Kubernetes** -> **Containers**).&#x20;

<figure><img src="../.gitbook/assets/screenshot-nimbusweb.me-2024.02.14-13_26_18.png" alt=""><figcaption><p>Clicking the Container <strong>Name</strong> on the <strong>Containers</strong> page to view a linked K8s job</p></figcaption></figure>

You can filter Container names by using the search field at the top of the page, as in this example:

<figure><img src="../.gitbook/assets/screenshot-nimbusweb.me-2024.02.14-13_29_20.png" alt=""><figcaption><p>Highlighted search field on the <strong>Containers</strong> page.</p></figcaption></figure>

## Editing a Kubernetes Job

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Job**.
2. Select the K8s job you want to edit.&#x20;
3. Click the options menu ( <img src="../.gitbook/assets/Kabab_three_Vertical_dots (5).png" alt="" data-size="line"> ) icon to the left of the job you want to edit and select **Edit**.

You can edit a job in the DuploCloud Portal and modify the following fields:

* **Cleanup After Finished in Seconds**
* **Other Spec Configuration**
* **Metadata Annotations**
* **Labels**

<figure><img src="../.gitbook/assets/edit.png" alt=""><figcaption><p><strong>Job</strong> page options menu with <strong>Edit</strong> option highlighted.</p></figcaption></figure>

## Deleting a Kubernetes Job

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Job**.
2. Select the K8s job you want to delete.&#x20;
3. Click the job options menu ( <img src="../.gitbook/assets/Kabab_three_Vertical_dots (5).png" alt="" data-size="line"> ) icon to the left of the job name and select **Delete**.

<figure><img src="../.gitbook/assets/delete.png" alt=""><figcaption><p>Job options menu with <strong>Delete</strong> option highlighted</p></figcaption></figure>
