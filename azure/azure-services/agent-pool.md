---
description: >-
  Meet performance demand in AKS workloads by organizing Azure agents into agent
  pools
---

# Agent pool

When you create agent pools to run Azure Kubernetes (AKS) workloads, you create groups of agents available to a pipeline. When you run the pipeline, the pipeline selects the agent that best meets the performance demands of that pipeline.

Agent pools can be scaled when the **Enable Autoscaling** option is selected in the DuploCloud Portal. Each agent pool contains nodes backed by virtual host machines.

Use the DuploCloud Portal **Hosts** page to create and manage Azure agent pools.

<figure><img src="../../.gitbook/assets/Agent_Pool_Azure (1).png" alt=""><figcaption><p><strong>Hosts</strong> page with <strong>Azure Agent Pool</strong> tab </p></figcaption></figure>

## Creating an agent pool

Create an Azure agent pool for an existing Host in the DuploCloud Portal:

1. Select **Devops** -> **Hosts** from the navigation menu.
2. Select the **Azure Agent Pool** tab.
3. Click **Add**.
4. Provide inputs for **Instance Type**, **Min Capacity**, and **Max Capacity** to scale the pool.
5. Click **Add**.  The **Azure Agent Pool** is created with Status displayed.

<figure><img src="../../.gitbook/assets/Agent_Pool_Azure_Agent_Pool_Created.png" alt=""><figcaption></figcaption></figure>

## Editing an agent pool

Edit an existing agent pool:

1. Select **Devops** -> **Hosts** from the navigation menu.
2. Select the **Azure Agent Pool** tab.
3. In the **Name** column on the form, select the name of the agent pool you want to edit.
4. Select **Actions** -> **Edit**.
5. In the **Update agent pool capacity** dialog, edit the pool configuration.
6. Click **Update**.





