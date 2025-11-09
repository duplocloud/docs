---
description: Create an Azure Managed SQL Instances in DuploCloud
---

# Azure Managed SQL Instances

An [Azure Managed SQL Instance](https://azure.microsoft.com/en-us/products/azure-sql/managed-instance/) offers a fully managed, scalable SQL database service. It simplifies database management by handling tasks like backups, patching, and scaling, so you can focus on your applications without worrying about infrastructure.

## Creating an Azure Managed SQL Instance

Complete the steps to create an Azure Managed SQL Instance in the DuploCloud Portal:

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database** -> **Managed Instances**.&#x20;
2.  Click **Add**. The **Create Managed SQL Instance** pane displays.\
    \


    <div align="left"><figure><img src="../../../../../.gitbook/assets/Screenshot (316).png" alt="" width="407"><figcaption><p>The <strong>Create Managed SQL Instance</strong> pane</p></figcaption></figure></div>
3. Complete the fields:

<table data-header-hidden><thead><tr><th width="155.3333740234375"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the Managed SQL Instance</td></tr><tr><td><strong>Username</strong></td><td>Create a username for the Managed SQL Instance</td></tr><tr><td><strong>Password</strong></td><td>Create a password for the Managed SQL Instance</td></tr><tr><td><strong>Service Tier</strong></td><td>Select your service tier (<code>General Purpose</code> or <code>Business Critical</code>)</td></tr><tr><td><strong>Hardware</strong></td><td>Select the hardware generation for the instance, such as Gen5</td></tr><tr><td><strong>vCore</strong></td><td>Select the number of virtual cores allocated to the instance</td></tr><tr><td><strong>Storage(GB)</strong></td><td>Select the amount of storage in gigabytes for the managed instance (e.g., <code>32 GB</code>)</td></tr><tr><td><strong>Subnet</strong></td><td>Specify the subnet where the managed instance will be deployed</td></tr></tbody></table>

4. Click **Submit** to generate the Managed SQL Instance.

## Additional Managed SQL Instance Options

Navigate directly to the Azure Portal to manage and configure a Managed SQL instance or delete a Managed SQL Instance from within the DuploCloud Portal:

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database** -> **Managed Instances**.&#x20;
2. Click the **menu icon** (<img src="../../../../../.gitbook/assets/menu icon (7).avif" alt="" data-size="line">) in the row of the Manages SQL Instance.
3. Select from the following options:&#x20;

<table data-header-hidden><thead><tr><th width="130.77783203125"></th><th></th></tr></thead><tbody><tr><td><strong>Azure Portal</strong></td><td>Navigate to the Azure portal to manage and configure your Managed SQL instance</td></tr><tr><td><strong>Delete</strong></td><td>Delete the Managed SQL Instance</td></tr></tbody></table>

<figure><img src="../../../../../.gitbook/assets/Screenshot (322) (1).png" alt=""><figcaption><p>The <strong>Managed Instances</strong> page in the DuploCloud Portal</p></figcaption></figure>
