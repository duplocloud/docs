---
description: >-
  Meet performance demand in AKS workloads by organizing Azure agents into agent
  pools
---

# Agent pool

When you create agent pools to run Azure Kubernetes (AKS) workloads, you create groups of agents available to a pipeline. When you run the pipeline, the pipeline selects the agent that best meets the performance demands of that pipeline.

Autoscaling can be enabled when creating agent pools in the DuploCloud Portal. Each agent pool contains nodes backed by virtual host machines.

## Prerequisites

To create an agent pool using availability zones, you must first create a [PostgreSQL Flexible Server subnet](databases/postgresql-flexible-server.md#create-a-postgresql-flexible-server-subnet-in-the-infrastructure) in the Infrastructure. For agent pools not using availability zones, skip this step.&#x20;

## Adding an agent pool

Create an Azure agent pool for an existing Host in the DuploCloud Portal.

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Hosts**.
2.  Select the **Azure Agent Pool** tab, and Click **Add**. The **Add Azure Agent Pool** page displays.\


    <figure><img src="../../.gitbook/assets/add agent pool AZ better.png" alt=""><figcaption><p>The <strong>Add Azure Agent Pool</strong> page in the DuploCloud Portal</p></figcaption></figure>
3. Provide inputs for the **Instance Type**, **Min Capacity**, **Max Capacity**, and **Desired Capacity** fields.
4. Enter allocation tags in the **Allocation Tags** field, if required.
5. Optionally, select **Enable Autoscaling**.
6. Optionally, select one or more availability zones from the **Availability Zones** list box. If you select availability zones, you must create a [PostgreSQL Flexible Server subnet](databases/postgresql-flexible-server.md#create-a-postgresql-flexible-server-subnet-in-the-infrastructure) in the Infrastructure before adding your agent pool. &#x20;
7.  Click **Add**. It may take some time to create the agent pool. When the agent pool is ready, **Succeeded** displays in the **Status** column. \


    <figure><img src="../../.gitbook/assets/agent pool success.png" alt=""><figcaption><p>The <strong>Azure Agent Pool</strong> tab on the <strong>Hosts</strong> page shows the <strong>DLJEGA1</strong> agent pool with <strong>Succeeded</strong> status</p></figcaption></figure>

## Editing an agent pool

Edit an agent pool:

1. Select **Cloud Services** -> **Hosts** from the navigation menu.
2. Select the **Azure Agent Pool** tab. The **Azure Agent Pool** page displays.
3. In the **Name** column, select the agent pool that you want to edit.
4.  Select the **Actions** menu and choose **Edit**.\


    <figure><img src="../../.gitbook/assets/edit agent pool.png" alt=""><figcaption><p>The <strong>Azure Agent Pool</strong> page with the <strong>Edit</strong> menu option highlighted</p></figcaption></figure>
5. In the **Update agent pool capacity** pane, edit the pool configuration.
6. Click **Update**.
