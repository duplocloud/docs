---
description: >-
  Meet performance demand in AKS workloads by organizing Azure agents into agent
  pools
---

# Agent pool

When you create agent pools to run Azure Kubernetes (AKS) workloads, you create groups of agents available to a pipeline. When you run the pipeline, the pipeline selects the agent that best meets the performance demands of that pipeline.

Agent pools can be[ autoscaled](../use-cases/hosts-vms/autoscaling/autoscaling-azure-agent-pools.md) when the **Enable Autoscaling** option is selected in the DuploCloud Portal. Each agent pool contains nodes backed by virtual host machines.

Use the DuploCloud Portal **Hosts** page to create and edit Azure agent pools.

## Creating an agent pool

Create an Azure agent pool for an existing Host in the DuploCloud Portal:

1. Select **Cloud Services** -> **Hosts** from the navigation menu.
2. Select the **Azure Agent Pool** tab. The **Azure Agent Pool** page is displayed.
3. Click **Add**. The **Add Azure Agent Pool** page is displayed.
4.  Provide inputs for the **Instance Type**, **Min Capacity**, and **Max Capacity** fields.\


    <figure><img src="../../.gitbook/assets/Add agent pool.png" alt=""><figcaption><p>Input fields on the <strong>Add Azure Ag</strong></p></figcaption></figure>
5. Optionally, select **Enable Autoscaling** to autoscale the pool.
6.  Click **Add**. When the agent pool is created, **Succeeded** is displayed in the **Status** column. It may take some time to create the agent pool.\


    <figure><img src="../../.gitbook/assets/agent pool success.png" alt=""><figcaption><p>Agent pool with <strong>Succeeded</strong> status</p></figcaption></figure>

## Editing an agent pool

Edit an agent pool:

1. Select **Cloud Services** -> **Hosts** from the navigation menu.
2. Select the **Azure Agent Pool** tab. The **Azure Agent Pool** page displays.
3. In the **Name** column, select the agent pool that you want to edit.
4.  Select the **Actions** menu and choose **Edit**.\


    <figure><img src="../../.gitbook/assets/edit agent pool.png" alt=""><figcaption><p>The <strong>Azure Agent Pool</strong> page with the <strong>Edit</strong> menu option highlighted</p></figcaption></figure>
5. In the **Update agent pool capacity** pane, edit the pool configuration.
6. Click **Update**.
