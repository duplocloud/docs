---
description: Configuring Azure Data Databricks in DuploCloud
---

# Databricks

[Azure Databricks](https://azure.microsoft.com/en-us/products/databricks/) is an Apache Spark-based analytics platform optimized for the Microsoft Azure cloud. It provides a collaborative environment for data engineers, data scientists, and analysts to work with big data and AI/ML workloads efficiently. With built-in integration for Azure services, Databricks simplifies data engineering, machine learning, and business analytics, making it an essential tool for organizations leveraging AI-driven insights.

## Adding an Azure Databricks Instance

DuploCloud now supports provisioning and managing Azure Databricks directly from the platform. Follow these steps to add a Databricks instance:

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **AI-ML**.
2.  Select the **Databricks** tab, and click **Add**. The **Add Databricks** pane displays.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (51).png" alt="" width="338"><figcaption><p>The <strong>Add Databricks</strong> pane</p></figcaption></figure></div>
3. Fill in the required fields:
   * **Name**: Provide a unique name for the Databricks instance.
   * **Tier**: Select the appropriate performance tier for the instance.
   * **Public IP**: Choose whether to enable or disable public IP access.
4. Click **Submit**. The Databricks instance will be provisioned, and you can manage it directly within the DuploCloud Platform.

<figure><img src="../../.gitbook/assets/Screenshot (53).png" alt=""><figcaption><p>The <strong>Databricks</strong> tab in the DuploCloud Portal</p></figcaption></figure>

## Managing an Azure Databricks Instance

After creating a Databricks instance, you can access additional management options:

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **AI-ML**.
2. Select the **Databricks** tab.
3. In the row corresponding to your Databricks instance, click the **menu icon** (<img src="../../.gitbook/assets/menu icon (1).avif" alt="" data-size="line">).
4. The following options are available:
   * **Copy**: Copy relevant details of the Databricks instance.
   * **Azure Portal**: Open the Databricks instance in the Azure Portal.
   * **Launch Workspace**: Access the Databricks workspace directly.
   * **Delete**: Remove the Databricks instance from DuploCloud.

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot (54).png" alt=""><figcaption><p>The actions menu for the db02 <strong>Databricks instance</strong> tab in the DuploCloud Portal</p></figcaption></figure></div>
