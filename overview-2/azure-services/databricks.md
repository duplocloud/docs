---
description: Configuring Azure Databricks in DuploCloud
---

# Databricks

[Azure Databricks](https://azure.microsoft.com/en-us/products/databricks/) is an Apache Spark-based analytics platform optimized for the Microsoft Azure cloud. It provides a collaborative environment for data engineers, data scientists, and analysts to work with big data and AI/ML workloads. Databricks connects easily with Azure services, making data work, machine learning, and analytics simpler. Azure Databricks can be provisioned and managed directly through the DuploCloud platform.

## Adding an Azure Databricks Instance

Complete the following steps to Add an Azure Databricks instance:

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **AI-ML**.
2.  Select the **Databricks** tab, and click **Add**. The **Add Databricks** pane displays.\
    \


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (51).png" alt="" width="338"><figcaption><p>The <strong>Add Databricks</strong> pane</p></figcaption></figure></div>
3. Fill in the fields:

<table data-header-hidden><thead><tr><th width="109.11114501953125">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a Databricks workspace name.</td></tr><tr><td><strong>Tier</strong></td><td>Choose between Standard or Premium. View Pricing details <a href="https://azure.microsoft.com/en-us/pricing/details/databricks/">here</a>.</td></tr><tr><td><strong>Disable Public IP</strong></td><td>If set to <code>Disabled</code>, no user access is permitted from the public internet.<br>If you set this to <code>Enabled</code>, users and REST API clients on the public internet can access Azure Databricks</td></tr><tr><td><strong>Vnet Integration</strong></td><td>Choosing <code>Enabled</code> allows you to deploy an Azure Databricks workspace in your virtual network. If enabled, you'll need to provide your <strong>Private Subnet</strong> and <strong>Public Subnet</strong>.</td></tr></tbody></table>

4. Click **Submit**. The Databricks instance will be provisioned.

<figure><img src="../../.gitbook/assets/Screenshot (53).png" alt=""><figcaption><p>The <strong>Databricks</strong> tab in the DuploCloud Portal</p></figcaption></figure>

## Managing an Azure Databricks Instance

After creating a Databricks instance, you can access additional management options:

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **AI-ML**.
2. Select the **Databricks** tab.
3. In the row corresponding to your Databricks instance, click the menu icon (<img src="../../.gitbook/assets/menu icon (1) (1).avif" alt="" data-size="line">).
4. Select from the following options:

<table data-header-hidden><thead><tr><th width="184.66668701171875"></th><th></th></tr></thead><tbody><tr><td><strong>Copy</strong></td><td>Copy relevant details of the Databricks instance</td></tr><tr><td><strong>Azure Portal</strong></td><td>Open the Databricks instance in the Azure Portal</td></tr><tr><td><strong>Launch Workspace</strong></td><td>Access the Databricks workspace directly</td></tr><tr><td><strong>Delete</strong></td><td>Delete the Databricks instance from DuploCloud</td></tr></tbody></table>

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot (54).png" alt=""><figcaption><p>The menu on the <strong>Databricks instance</strong> tab in the DuploCloud Portal</p></figcaption></figure></div>
