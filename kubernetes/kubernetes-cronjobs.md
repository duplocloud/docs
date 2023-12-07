---
description: >-
  Schedule a Kubernetes Job in AWS and GCP by creating a CronJob in the
  DuploCloud Portal
---

# Kubernetes CronJobs

A [Kubernetes ](https://kubernetes.io/)CronJob is a variant of a [Kubernetes Job](kubernetes-jobs.md), with the exception that you can schedule a CronJob to run at periodic intervals.

See the Kubernetes documentation on [CronJobs](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/) for more information.

## Creating a Kubernetes CronJob in the DuploCloud Portal

1. In the DuploCloud Portal, navigate to **DevOps** -> **Containers** -> **EKS/Native**.
2. Click the **K8s CronJob** tab.
3. Click **Add**. The **Add Kubernetes CronJob** page displays.
4. In the **Basic Options** step, specify the Kubernetes CronJob **Name**.
5. In the **Schedule** field, specify the Cron Schedule in Cron Format. Click the Info Tip icon       ( <img src="../.gitbook/assets/info_tip_black.png" alt="" data-size="line"> ) for examples. When specifying a **Schedule** in Cron Format, ensure you separate each value with a space. For example, `0 0 * * 0` is a valid Cron Format input; `00**0` is not. See the [Kubernetes documentation](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/#writing-a-cronjob-spec) for detailed information about Cron Format.
6.  In the **Container - 1** area, specify the **Container Name** and associated **Docker Image**.\


    <figure><img src="../.gitbook/assets/j15.png" alt=""><figcaption><p>Add Kubernetes CronJob page</p></figcaption></figure>


7.  In the **Command** field, specify the command attributes for **Container - 1**. Click the Info Tip icon       ( <img src="../.gitbook/assets/info_tip_black.png" alt="" data-size="line"> ) for examples. Select and **Copy** commands as needed.\


    <div align="left">

    <figure><img src="../.gitbook/assets/j16.png" alt=""><figcaption><p>Examples for <strong>Command</strong> field in <strong>Container - 1</strong> area of <strong>Add Kubernetes CronJob</strong> page<br></p></figcaption></figure>

    </div>



    <div align="left">

    <figure><img src="../.gitbook/assets/j17.png" alt=""><figcaption><p>Completed <strong>Command</strong> field for <strong>Container - 1</strong> </p></figcaption></figure>

    </div>


8.  To run the Job to completion, you must specify a Kubernetes [Init Container](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/).  Click the **Add Container** <img src="../.gitbook/assets/chevron_Down_arrow.png" alt="" data-size="line">button and select the **Add Init Container** option. The **Init Container - 1** area displays.\


    <div align="left">

    <figure><img src="../.gitbook/assets/j18.png" alt=""><figcaption><p><strong>Add Init Container</strong> option on <strong>Add Container</strong> button in <strong>Container - 1</strong> area</p></figcaption></figure>

    </div>



    <figure><img src="../.gitbook/assets/j23.png" alt=""><figcaption><p><strong>Init Container - 1</strong> area</p></figcaption></figure>


9. In the **Init Container - 1** area, specify the **Container Name** and associated **Docker Image**.
10. Click **Next** to open the **Advanced Configuration** step.
11. In the **Other Spec Configuration** field, specify the Job spec (in YAML) for **Init Container - 1**. Click the Info Tip icon       ( <img src="../.gitbook/assets/info_tip_black.png" alt="" data-size="line"> ) for examples. Select and **Copy** commands as needed.\


    <div align="left">

    <figure><img src="../.gitbook/assets/j21.png" alt=""><figcaption><p>Examples for <strong>Other Spec Configuration</strong> field in <strong>Advanced Configuration</strong> step for <strong>Init Container - 1</strong><br></p></figcaption></figure>

    </div>

    <div align="left">

    <figure><img src="../.gitbook/assets/j22.png" alt=""><figcaption><p>Completed <strong>Other Spec Configuration</strong> field for <strong>Init Container - 1</strong> <br></p></figcaption></figure>

    </div>
12. Click **Create**. The K8s CronJob is created and displayed in the **K8s CronJob** tab and will be run according to the Schedule you specified.&#x20;

<div align="left">

<figure><img src="../.gitbook/assets/j24.png" alt=""><figcaption><p><strong>K8s CronJob</strong> tab displaying Kubernetes Job <strong>PERL123</strong> </p></figcaption></figure>

</div>

## Viewing a Kubernetes CronJob&#x20;

1. In the DuploCloud Portal, navigate to **DevOps** -> **Containers** -> **EKS/Native**.
2. Click the **K8s CronJob** tab.
3. Select the K8s Job you want to view and click the **Overview, Schedule**, and **Details** tabs for more information about the job schedule and job history.&#x20;

You can also view details of a Kubernetes Job by clicking the Job Menu Icon ( <img src="../.gitbook/assets/Kabab_three_Vertical_dots.png" alt="" data-size="line"> ) icon to the left of the Job name and selecting **View**.

<div align="left">

<figure><img src="../.gitbook/assets/j25.png" alt=""><figcaption><p><strong>Schedule</strong> tab for Kubernetes Job <strong>PERL123</strong></p></figcaption></figure>

</div>

<figure><img src="../.gitbook/assets/j26.png" alt=""><figcaption><p>Job Option Menu with <strong>View</strong> option highlighted</p></figcaption></figure>

### Using the Container page to view linked Kubernetes Jobs

You can also view K8s Job **Overview** and **Details** by clicking the Container **Name** in the **Containers** tab (**DevOps** -> **Containers** -> **EKS/Native** -> **Containers**). \


<div align="left">

<figure><img src="../.gitbook/assets/j29.png" alt=""><figcaption><p>Clicking the Container <strong>Name</strong> on the <strong>Containers</strong> page to view a linked K8s CronJob</p></figcaption></figure>

</div>

You can filter Container Names by using the search field at the top of the page, as in this example:

<figure><img src="../.gitbook/assets/j30.png" alt=""><figcaption><p>Highlighted search field on the <strong>Containers</strong> page </p></figcaption></figure>

## Editing a Kubernetes Job

1. In the DuploCloud Portal, navigate to **DevOps** -> **Containers** -> **EKS/Native**.
2. Click the **K8s Job** tab.
3. Select the K8s Job you want to edit.&#x20;
4. Click the Job Options Menu ( <img src="../.gitbook/assets/Kabab_three_Vertical_dots.png" alt="" data-size="line"> ) icon to the left of the Job name and select **Edit**.

You can Edit a Kubernetes Job in the DuploCloud Portal and modify the following fields:

* Cleanup After Finished in Seconds
* Other Spec Configuration
* Metadata Annotations
* Labels

<figure><img src="../.gitbook/assets/j27.png" alt=""><figcaption><p>Job Option Menu with <strong>Edit</strong> option highlighted</p></figcaption></figure>

## Deleting a Kubernetes Job

1. In the DuploCloud Portal, navigate to **DevOps** -> **Containers** -> **EKS/Native**.
2. Click the **K8s Job** tab.
3. Select the K8s Job you want to edit.&#x20;
4. Click the Job Options Menu ( <img src="../.gitbook/assets/Kabab_three_Vertical_dots.png" alt="" data-size="line"> ) icon to the left of the Job name and select **Delete**.

<figure><img src="../.gitbook/assets/j28.png" alt=""><figcaption><p>Job Option Menu with <strong>Delete</strong> option highlighted</p></figcaption></figure>

