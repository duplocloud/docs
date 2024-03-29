---
description: >-
  Schedule a Kubernetes Job in AWS and GCP by creating a CronJob in the
  DuploCloud Portal
---

# CronJobs

A [Kubernetes ](https://kubernetes.io/)CronJob is a variant of a [Kubernetes Job](jobs.md), with the exception that you can schedule a CronJob to run at periodic intervals.

See the Kubernetes documentation on [CronJobs](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/) for more information.

## Creating a Kubernetes CronJob in the DuploCloud portal

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **CronJob**.
2. Click **Add**. The **Add Kubernetes CronJob** page displays.
3. In the **Basic Options** step, specify the Kubernetes CronJob **Name**.
4. In the **Schedule** field, specify the Cron Schedule in Cron Format. Click the Info Tip icon for examples. When specifying a **Schedule** in Cron Format, ensure you separate each value with a space. For example, `0 0 * * 0` is a valid Cron Format input; `00**0` is not. See the [Kubernetes documentation](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/#writing-a-cronjob-spec) for detailed information about Cron Format.
5. In the **Container - 1** area, specify the **Container Name** and associated **Docker Image**.

<figure><img src="../.gitbook/assets/cron1.png" alt=""><figcaption><p><strong>Add Kubernetes CronJob</strong> page</p></figcaption></figure>

6.  In the **Command** field, specify the command attributes for **Container - 1**. Click the Info Tip icon for examples. Select and **Copy** commands as needed.\


    <figure><img src="../.gitbook/assets/cron2.png" alt=""><figcaption><p>Examples for <strong>Command</strong> field in <strong>Container - 1</strong> area of <strong>Add Kubernetes CronJob</strong> page.<br></p></figcaption></figure>

    <figure><img src="../.gitbook/assets/cron3.png" alt=""><figcaption><p>Completed <strong>Command</strong> field for <strong>Container - 1.</strong></p></figcaption></figure>
7.  To run the CronJob to completion, you must specify a Kubernetes [Init Container](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/).  Click the **Add Container** <img src="../.gitbook/assets/chevron_Down_arrow.png" alt="" data-size="line">button and select the **Add Init Container** option. The **Init Container - 1** area displays.\


    <figure><img src="../.gitbook/assets/cron4.png" alt=""><figcaption><p><strong>Add Init Container</strong> option on <strong>Add Container</strong> button in <strong>Container - 1</strong> area.<br></p></figcaption></figure>

    <figure><img src="../.gitbook/assets/cron5.png" alt=""><figcaption><p><strong>Init Container - 1</strong> area.</p></figcaption></figure>
8. In the **Init Container - 1** area, specify the **Container Name** and associated **Docker Image**.
9. Click **Next** to open the **Advanced Configuration** step.
10. In the **Other Spec Configuration** field, specify the job spec (in YAML) for **Init Container - 1**. Click the Info Tip icon ( <img src="../.gitbook/assets/info_tip_black.png" alt="" data-size="line"> ) for examples. Select and **Copy** commands as needed

<figure><img src="../.gitbook/assets/cron6 (1).png" alt=""><figcaption><p>Examples for <strong>Other Spec Configuration</strong> field in <strong>Advanced Configuration</strong> step for <strong>Init Container - 1.</strong></p></figcaption></figure>

<figure><img src="../.gitbook/assets/cron7.png" alt=""><figcaption><p>Completed <strong>Other Spec Configuration</strong> field for <strong>Init Container - 1.</strong></p></figcaption></figure>

8.  Click **Create**. The K8s CronJob is created and displayed on the **CronJob** page and will be run according to the schedule you specified. \


    <figure><img src="../.gitbook/assets/cron8.png" alt=""><figcaption><p><strong>K8s CronJob</strong> tab displaying Kubernetes Job <strong>MYCRONJOB.</strong></p></figcaption></figure>

## Viewing a Kubernetes CronJob&#x20;

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **CronJob**.
2. Select the CronJob you want to view and click the **Overview, Schedule**, and **Details** tabs for more information about the job schedule and job history.&#x20;

You can also view details of a Kubernetes CronJob by clicking on the **menu icon** ( <img src="../.gitbook/assets/Kabab_three_Vertical_dots (5).png" alt="" data-size="line"> ) icon to the left of the job name and selecting **View**.



<figure><img src="../.gitbook/assets/cron9.png" alt=""><figcaption><p><strong>Overview</strong> tab for Kubernetes Job <strong>MYCRONJOB.</strong></p></figcaption></figure>

<figure><img src="../.gitbook/assets/cronview.png" alt=""><figcaption><p>CronJob options menu with <strong>View</strong> option highlighted.</p></figcaption></figure>

### Using the Container page to view linked Kubernetes CronJobs

You can also view CronJobs linked to containers by clicking the container **Name** on the **Containers** page (**Kubernetes** -> **Containers**). \


<div align="left">

<figure><img src="../.gitbook/assets/j29.png" alt=""><figcaption><p>Clicking the Container <strong>Name</strong> on the <strong>Containers</strong> page to view a linked K8s CronJob</p></figcaption></figure>

</div>

You can filter container names by using the search field at the top of the page, as in this example:



<figure><img src="../.gitbook/assets/search containers.png" alt=""><figcaption><p>Highlighted search field on the <strong>Containers</strong> page </p></figcaption></figure>

## Editing a Kubernetes CronJob

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **CronJob**.
2. Select the K8s CronJob you want to edit.&#x20;
3. Click the **options menu** ( <img src="../.gitbook/assets/Kabab_three_Vertical_dots (5).png" alt="" data-size="line"> ) icon to the left of the CronJob name and select **Edit**.

You can edit a Kubernetes Job in the DuploCloud Portal and modify the following fields:

* **Cleanup After Finished in Seconds**
* **Other Spec Configuration**
* **Metadata Annotations**
* **Labels**

<figure><img src="../.gitbook/assets/cron edit.png" alt=""><figcaption><p>CronJob options menu with <strong>Edit</strong> option highlighted</p></figcaption></figure>

## Deleting a Kubernetes CronJob

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **CronJob.**
2. Select the K8s CronJob you want to delete.&#x20;
3. Click the Job Options Menu ( <img src="../.gitbook/assets/Kabab_three_Vertical_dots (5).png" alt="" data-size="line"> ) icon to the left of the Job name and select **Delete**.

<figure><img src="../.gitbook/assets/cron delete.png" alt=""><figcaption><p>Job options menu with <strong>Delete</strong> option highlighted</p></figcaption></figure>

