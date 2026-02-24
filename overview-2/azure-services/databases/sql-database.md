---
description: Create a Microsoft SQL (MSSQL) Server database in DuploCloud
---

# Microsoft SQL Server (MSSQL)

DuploCloud supports the deployment and management of [Microsoft SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) (MSSQL) on Azure. You can use the DuploCloud Portal to create MSSQL Servers, add databases, and apply network and security configurations such as firewall rules, private endpoints, and virtual network rules.

## Prerequisites

### Enable public access for MSSQL Servers

To create an MSSQL Server with public access, you must first enable a Tenant setting that allows public network access for databases and cache servers. If public access is not required, you can skip this step and proceed directly to [create an MSSQL Server](sql-database.md#creating-an-mssql-server).

1. From the DuploCloud Portal, navigate to **Administrator** -> **Tenants**.
2. Select the Tenant from the **NAME** column.&#x20;
3. Select the **Settings** tab, and click **Add**. The **Add Tenant Feature** pane displays.
4. From the **Select Feature** list box, select **Allow Public Network Access for Databases and Cache Servers**.
5. Enable the setting, and click **Add**. Public access is enabled.&#x20;

## Creating an MSSQL Server

Create a new Microsoft SQL Server instance in your tenant to host one or more SQL databases for your applications.

1. Select the Tenant from the **Tenant** list box.&#x20;
2. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database** ->  **MSSQLServer**.
3. Click **Add**. The **Add SQL Server** pane displays.
4. Provide a name for the MSSQL Server database, your username and password, and database version information.&#x20;
5. From the **Public Access** list box, select **Enabled** or **Disabled**. If **Enabled** is not available, complete the steps above under **Prerequisites** to [enable this option](sql-database.md#enable-public-access-for-databases-in-tenant-settings).  &#x20;
6. Click **Submit**. The MSSQL Server database is created.&#x20;

<div align="left"><img src="../../../.gitbook/assets/Screenshot (700).png" alt="Create My SQL Server" width="438"></div>

## **Adding an SQL database**

After creating an MSSQL Server, you must add one or more SQL databases to store your application data.

1. Select the Tenant from the **Tenant** list box.
2. Navigate to **Cloud Services** → **Database** → **MSSQL Server**.
3. Select the MSSQL Server from the **NAME** column.
4.  In the **Databases** tab, click **Add**. The **Create SQL Database** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (760).png" alt="" width="405"><figcaption><p><strong>Create SQL Database</strong> pane</p></figcaption></figure></div>
5. Complete the following fields:

<table data-header-hidden><thead><tr><th width="157.99993896484375">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the database. </td></tr><tr><td><strong>Use Elastic Pool</strong></td><td>Select whether to use an elastic pool. Default is <strong>No</strong>.</td></tr><tr><td><strong>Service Tier</strong></td><td>Select the service tier.</td></tr><tr><td><strong>SKU Name</strong></td><td>Select the SKU name.</td></tr><tr><td><strong>Collation</strong></td><td>Optionally, enter the collation setting.</td></tr></tbody></table>

6. Click **Submit** to create the database.

## **Updating the backup retention period for a database**

The default backup retention period for an SQL database is 7 days. You can update this setting to retain backups for up to 35 days.

1. Select the Tenant from the **Tenant** list box.
2. Navigate to **Cloud Services** → **Database** → **MSSQLServer**.
3. Select the MSSQL Server from the **NAME** column.
4. Select the **Databases** tab.
5. Click the menu icon (<img src="../../../.gitbook/assets/menu icon (22).avif" alt="" data-size="line">) next to the database and select **Update Short Term Retention**. The **Update Backup Retention Period** pane displays.

<div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (761).png" alt="" width="406"><figcaption><p><strong>Update Backup Retention Period</strong> pane</p></figcaption></figure></div>

6. Enter a value between **1** and **35** days and click **Save**.

{% hint style="info" %}
The backup retention period cannot be configured for the `master` database.
{% endhint %}

## Viewing MSSQL Server and database details

1. Select the Tenant from the **Tenant** list box.
2. In the DuploCloud Portal, navigate to **Cloud Services** → **Database** → **MSSQLServer**.
3.  Select the MSSQL Server from the **NAME** column. The MSSQL Server details page displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (778).png" alt=""><figcaption><p><strong>MSSQL Server</strong> page</p></figcaption></figure></div>
4. Use one of the following options to manage the server and its databases:

Use the **tabs** to view server details:

<table data-header-hidden><thead><tr><th width="177.5555419921875">Option</th><th>Description</th></tr></thead><tbody><tr><td><strong>Databases</strong></td><td>View or manage the databases associated with this server.</td></tr><tr><td><strong>Elastic Pools</strong></td><td>View or configure elastic pool settings, if applicable.</td></tr><tr><td><strong>Private Endpoints</strong></td><td>View or manage private network connections.</td></tr><tr><td><strong>Virtual Network Rules</strong></td><td>View or manage subnet-based access restrictions. This tab is only visible when public access is <strong>enabled</strong>.</td></tr><tr><td><strong>Firewall Rules</strong></td><td>View or manage IP-based firewall rules. This tab is only visible when public access is <strong>enabled</strong>.</td></tr></tbody></table>

You can also use the **Actions** button at the top right of the page:

<table data-header-hidden><thead><tr><th width="182.88885498046875">Action</th><th>Description</th></tr></thead><tbody><tr><td><strong>Azure Portal</strong></td><td>Open the server directly in the Azure Portal.</td></tr><tr><td><strong>Delete SQL Server</strong></td><td>Delete the server if no databases remain.</td></tr></tbody></table>

To manage an individual database, go to the **Databases** tab and click the menu icon (<img src="../../../.gitbook/assets/menu icon (23).avif" alt="" data-size="line">) next to the database name:

<table data-header-hidden><thead><tr><th width="189.99993896484375">Option</th><th>Description</th></tr></thead><tbody><tr><td><strong>Edit</strong></td><td>Update the database name or settings.</td></tr><tr><td><strong>Update Short Term Retention</strong></td><td>Configure the backup retention period for the database.</td></tr><tr><td><strong>Delete</strong></td><td>Remove the database from the server.</td></tr></tbody></table>

{% hint style="info" %}
The `master` database is managed by Azure and cannot be edited or deleted.
{% endhint %}

## Adding private endpoints

A private endpoint is a network interface that connects you privately and securely to your MSSQL Server. This ensures that the traffic between your virtual network and the MSSQL database travels entirely without using the public internet.

1. Select the Tenant from the **Tenant** list box.&#x20;
2. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database** ->  **MSSQLServer.**
3. Select the MSSQL Server database from the **NAME** column.&#x20;
4.  Select the **Private Endpoints** tab, and click **Add**. The **Add Private Endpoint** pane displays. <br>

    <div align="left"><figure><img src="../../../.gitbook/assets/private endpoint.png" alt="" width="375"><figcaption><p>The <strong>Add Private Endpoint</strong> pane</p></figcaption></figure></div>
5. Add a name and select a subnet for your private endpoint.&#x20;
6. Click **Submit**. The private endpoint is created and accessible via the selected subnet. &#x20;

## **Configuring** elastic pools

Azure SQL Database Elastic Pools provide cost-effective database resource management by pooling multiple databases together and sharing resources based on their individual needs.

Configure Azure Elastic Pools for an MSSQL Server in the DuploCloud Portal:

1. Select the Tenant from the **Tenant** list box.&#x20;
2. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database** ->  **MSSQLServer.**
3. Select the MSSQL Server database from the **NAME** column.&#x20;
4.  Select the **Elastic Pools** tab, and click **Add**. The **Add SQL Elastic Pool** pane displays. <br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (705).png" alt=""><figcaption><p>The <strong>Add SQL Elastic Pool</strong> pane</p></figcaption></figure></div>
5. Enter a name for the elastic pool and configure the  SQL Elastic Pool (select your **Service Tier**, **Sku Name**, **Max Storage Size**).&#x20;
6.  Click **Submit**. The elastic pool is created. <br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (706).png" alt=""><figcaption></figcaption></figure></div>

## Setting virtual network rules

Virtual network rules restrict access to your MSSQL Server to specific subnets within a virtual network, enhancing security and network isolation. Public access must be enabled to add virtual network rules.&#x20;

1. Select the Tenant from the **Tenant** list box.&#x20;
2. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database** ->  **MSSQL Server.**
3. Select the MSSQL Server from the **NAME** column.&#x20;
4. Select the **Virtual Network Rules** tab, and click **Add**. The **Add New Virtual Network Rule** pane displays.&#x20;
5. Add a name for the virtual network rule, and select the subnet. Click **Create**. The virtual network rule is created.

<div align="left"><figure><img src="../../../.gitbook/assets/VN rule.png" alt=""><figcaption><p><strong>Virtual Network Rule</strong> tab on the <strong>MSSQL Server</strong> page. </p></figcaption></figure></div>

## Setting firewall rules

Firewall rules for an MSSQL Server control access by allowing or denying traffic based on IP addresses. These rules help secure your databases by restricting access to trusted sources. Public access must be enabled to add firewall rules.&#x20;

1. Select the Tenant from the **Tenant** list box.&#x20;
2. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database** ->  **MSSQL Server.**
3. Select the MSSQL Server database from the **NAME** column.&#x20;
4.  Select the **Firewall Rules** tab, and click **Add**. The **Add New SQL Server Firewall Rule** pane displays. <br>

    <div align="left"><figure><img src="../../../.gitbook/assets/fw rules.png" alt="" width="367"><figcaption><p><strong>Add New SQL Server Firewall Rule</strong> pane</p></figcaption></figure></div>
5. Add a name for the firewall rule, and specify the starting and ending IP addresses that should be allowed to access your MSSQL database.
6.  Click **Create**. The firewall rule is added to the server.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/firewall rule success.png" alt=""><figcaption><p><strong>Firewall Rule</strong> tab on the <strong>MSSQL Server</strong> page. </p></figcaption></figure></div>
