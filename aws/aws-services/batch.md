---
description: Run AWS batch jobs without installing software or servers
---

# Batch

You can perform [AWS batch job](https://docs.aws.amazon.com/batch/latest/userguide/jobs.html) processing directly in the DuploCloud Portal without the additional overhead of installed software, allowing you to focus on analyzing results and diagnosing problems.

## Create Batch Job Scheduling Policies&#x20;

Create scheduling policies to define when your batch job runs.&#x20;

1. From the DuploCloud Portal **DevOps** -> **Batch** page, click the **Scheduling Policies** tab.
2.  Click **Add**. The **Create Batch Scheduling Policy** page displays.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/scheduling new 2.png" alt=""><figcaption><p><strong>Create Batch Queue</strong> page in DuploCloud Portal</p></figcaption></figure>

    </div>



    <div align="left">

    <figure><img src="../../.gitbook/assets/scheduling new 1.png" alt=""><figcaption><p>AWS Batch <strong>Create Batch Scheduling Policy</strong> page in DuploCloud Portal</p></figcaption></figure>

    </div>


3. In the **Create Batch Scheduling Policy** page, create batch job scheduling policies using the [AWS documentation](https://docs.aws.amazon.com/batch/latest/userguide/scheduling-policies.html). The fields in the AWS documentation map to the fields on the DuploCloud **Create Batch Scheduling Policy** page.
4. Click **Create**.

## Configure Compute Environments

[AWS compute environments](https://docs.aws.amazon.com/batch/latest/userguide/getting-started-eks.html#getting-started-eks-step-1) (Elastic Compute Cloud \[EC2] instances) map to DuploCloud Infrastructures. The settings and constraints in the computing environment define how to configure and automatically launch the instance.

1. In the DuploCloud Portal, navigate to **DevOps** -> **Batch**.&#x20;
2. Click the **Compute Environments** tab.
3.  Click **Add**. The **Add Batch Environment** page displays.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/newcompute environment.png" alt=""><figcaption><p>AWS Batch <strong>Add Batch Environment</strong> page in DuploCloud Portal<br></p></figcaption></figure>

    </div>

    <div align="left">

    <figure><img src="../../.gitbook/assets/newcomputeenv2 (1).png" alt=""><figcaption><p>AWS Batch <strong>Add Batch Environment</strong> page in DuploCloud Portal</p></figcaption></figure>

    </div>
4. In the **Compute Environment Name** field, enter a unique name for your environment.
5. In the **Type** field, select the environment type (**On-Demand**, **Spot**, **Fargate**, etc.).
6. Modify additional defaults on the page, as needed, or add configuration parameters in **Other Configurations**.&#x20;
7. Click **Create**.

## Create Batch Job Queues

After you define job definitions, create queues in which your batch jobs are run. For more information about batch job queues, see the [AWS instructions for creating a job queue](https://docs.aws.amazon.com/batch/latest/userguide/create-job-queue-ec2.html).

1. From the DuploCloud Portal **DevOps** -> **Batch** page, click the **Queues** tab.
2.  Click **Add**. The **Create Batch Queue** page displays.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/new batch queue.png" alt=""><figcaption><p>AWS Batch <strong>Create Batch Queue</strong> page in DuploCloud Portal</p></figcaption></figure>

    </div>
3. In the **Create Batch Queue** page, create batch job queues using the [AWS documentation](https://docs.aws.amazon.com/batch/latest/userguide/job\_queues.html). The fields in the AWS documentation map to the fields on the DuploCloud **Create Batch Queue** page.
4. Click **Create**.

{% hint style="info" %}
For **Priority**, enter a whole number. Job queues with a higher priority are run before those with a lower priority associated with the same compute environment.&#x20;
{% endhint %}

## Create Batch Job Definitions

Before you can run AWS batch jobs, you need to create job definitions specifying how batch jobs are run.

1. From the DuploCloud Portal **DevOps** -> **Batch** page, click the **Job Definitions** tab.
2.  Click **Add**. The **Create** **Batch Job Definition** page displays.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/new batch job definition.png" alt=""><figcaption><p>AWS Batch <strong>Create Batch Job Definition</strong> page in DuploCloud Portal<br></p></figcaption></figure>

    </div>

    <div align="left">

    <figure><img src="../../.gitbook/assets/batchdef2.png" alt=""><figcaption><p>The <strong>Batch Job Definition</strong> configuration screen in the DuploCloud Portal</p></figcaption></figure>

    </div>


3. In the **Create Batch Job Definition** page, define your batch jobs using the [AWS documentation](https://docs.aws.amazon.com/batch/latest/userguide/job\_definitions.html). The fields in the AWS documentation map to the fields on the DuploCloud **Create Batch Job Definition** page.
4. Click **Create**.

## Create a Batch Job

Add a job for AWS batch processing. See the [AWS documentation](https://docs.aws.amazon.com/batch/latest/userguide/jobs.html) for more information about batch jobs.

1. After you [configure your compute environment](batch.md#configuring-compute-environments), In the DuploCloud Portal, click the **Jobs** tab.&#x20;
2.  Click **Add**. The **Add Batch Job** page displays.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/new batch job image.png" alt=""><figcaption><p>AWS Batch <strong>Add Batch Job</strong> page in DuploCloud Portal</p></figcaption></figure>

    </div>
3. In the **Add Batch Job** page, define a **Job Name**, **Job Definition**, **Job Queue**, and **Job Properties**.
4. Click **Create**.

## Run AWS Batch jobs

Use the [AWS Best Practices Guide](https://docs.aws.amazon.com/batch/latest/userguide/best-practices.html) for information about running your AWS Batch jobs.
