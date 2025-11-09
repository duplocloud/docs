---
description: Provision and manage Azure CosmosDB accounts and databases in DuploCloud
---

# CosmosDB

Azure CosmosDB is a globally distributed, multi-model NoSQL database service designed for high availability, low latency, and seamless scalability. It supports various data models such as key-value, document, graph, and column-family, making it ideal for modern cloud-native applications.

In DuploCloud, you can provision and manage Azure CosmosDB accounts, which serve as top-level containers for your databases. Each account defines key configurations like capacity mode, public access, and authentication. Once an account is created, you can add multiple databases within it to organize and store your application data.

This page describes how to provision and manage Azure CosmosDB accounts and resources in the DuploCloud Portal.

## Adding an Azure CosmosDB Account

1. In the DuploCloud Portal, navigate to **Cloud Services** → **Databases** → **CosmosDB**.
2.  Click **Add**. The **Create CosmosDB Account** pane displays.\


    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (573).png" alt=""><figcaption><p><strong>Create CosmosDB Account</strong> pane</p></figcaption></figure></div>
3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="243.33331298828125">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a friendly name for the CosmosDB account.</td></tr><tr><td><strong>Capacity Mode</strong></td><td>Choose either <strong>Provisioned throughput</strong> or <strong>Serverless</strong>.</td></tr><tr><td><strong>Public Access</strong></td><td>Select whether public network access is <strong>Enabled</strong> or <strong>Disabled</strong>.</td></tr><tr><td><strong>Enable Free Tier</strong></td><td>Enable Azure’s free-tier capacity, if needed.</td></tr><tr><td><strong>Key-based Authentication</strong></td><td>Enable key-based access credentials for CosmosDB, if needed.</td></tr></tbody></table>

4. Click **Submit** to create the account. Once created, the CosmosDB account appears in the list and can be managed or referenced in your infrastructure deployments.

## Viewing a CosmosDB Account

1. In the DuploCloud Portal, navigate to **Cloud Services** → **Databases** → **CosmosDB**.
2. Click on the name of the CosmosDB account in the **NAME** column.
3.  Select the **Databases**, **Private Endpoints**, or **Details** tab to view account details. \


    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (576).png" alt=""><figcaption><p><strong>Details</strong> tab for the <code>cosmodb-1243</code> CosmosDB account</p></figcaption></figure></div>

## Managing a CosmosDB Account

After creating a CosmosDB account in DuploCloud, you can view, edit, or delete the account:

1. In the DuploCloud Portal, navigate to **Cloud Services** → **Databases** → **CosmosDB**.
2.  Click the menu icon (<img src="../../../../.gitbook/assets/menu icon (18) (1).avif" alt="" data-size="line">) in the row of the CosmosDB account you want to manage.\


    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (577) (1).png" alt=""><figcaption><p><strong>CosmosDB</strong> page with the menu options highlighted</p></figcaption></figure></div>
3.  Choose from the following options:

    * **JSON:** View the raw JSON configuration of the CosmosDB account.
    * **Edit:** Modify the account settings.
    * **Delete:** Permanently remove the CosmosDB account.\


    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (578).png" alt=""><figcaption><p><strong>Details</strong> tab for the <code>cosmodb-1243</code> Cosmosdb account</p></figcaption></figure></div>

## Adding a Database in Data Explorer

1. In the DuploCloud Portal, navigate to **Cloud Services** → **Databases** → **CosmosDB**.
2. Select the CosmosDB account from the **NAME** column.
3. Select the **Data Explorer** tab.
4.  Click **Add**. The **Add CosmosDB Database** pane displays. \


    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (579).png" alt=""><figcaption><p><strong>Add CosmosDB Database</strong> pane</p></figcaption></figure></div>
5. Enter a **Name** for the database.
6. Click **Create** to add the database.

## Adding a Private Endpoint

1. In the DuploCloud Portal, navigate to **Cloud Services** → **Databases** → **CosmosDB**.
2. Select the CosmosDB account from the **NAME** column.
3. Select the **Private Endpoints** tab.
4.  Click **Add**. The **Add Private Endpoint** pane displays. \


    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (580).png" alt=""><figcaption><p><strong>Add Private Endpoint</strong> pane</p></figcaption></figure></div>
5. Provide a **Name** for the endpoint
6. Select the **Subnet** where the endpoint will be created
7. Click **Create** to establish the private endpoint.
