---
description: Configure CloudFront Key-Value Stores in DuploCloud
---

# CloudFront Key-Value Stores

CloudFront Key-Value Stores let you manage key-value data that can be accessed by CloudFront Functions to implement personalized, dynamic behaviors at the edge.

## Adding a CloudFront Key-Value Store

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Networking**.
2. Select the **CloudFront** tab.
3. Select the **Key-Value Stores** tab.
4. Click **Add**. The **Add Key-Value Store** pane displays.
5. Complete the following fields.

<table data-header-hidden><thead><tr><th width="186.4444580078125">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for the Key-Value Store.</td></tr><tr><td><strong>Description</strong></td><td>Provide a brief description of the store’s purpose.</td></tr></tbody></table>

***

5. Click **Create** to create the Key-Value Store. Once created, you can add key-value pairs (in AWS Console) to this store and associate it with CloudFront Functions for dynamic content delivery.

## Managing a Key-Value Store

After creating a Key-Value Store, you can view and edit its key-value pairs, export them for backup or review, associate the store with CloudFront Functions to enable dynamic edge logic, or delete the store if it’s no longer needed.

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Networking**.
2. Select the **CloudFront** tab.
3. Select the **Key-Value Stores** tab.
4. Click the menu icon (<img src="../../../../.gitbook/assets/menu icon (30).avif" alt="" data-size="line">) next to the Key-Value Store you want to manage.
5. Select one of the following options:

<table data-header-hidden><thead><tr><th width="244.22216796875">Option</th><th>Description</th></tr></thead><tbody><tr><td><strong>Delete</strong></td><td>Permanently removes the selected Key-Value Store. This action cannot be undone.</td></tr><tr><td><strong>JSON</strong></td><td>View or export the key-value pairs in JSON format. This allows you to review all entries at once or back them up externally.</td></tr><tr><td><strong>Console</strong></td><td>Open the key-value editor to add new pairs, modify existing ones, or delete entries. Save your changes before exiting the editor.</td></tr><tr><td><strong>Associate Function</strong></td><td>Link the Key-Value Store to a CloudFront Function. This grants the function permission to access the store during edge processing. Once associated, the function can use the Key-Value Store API to retrieve or update values in real time, enabling dynamic behaviors like feature flagging, routing logic, or custom headers without redeploying function code. The association also ensures the function only has access to explicitly linked stores, improving security and data governance.</td></tr><tr><td><strong>Disassociate Function</strong></td><td>Remove the link between this Key-Value Store and any associated CloudFront Function. Use this if you want to stop the function from accessing the store.</td></tr></tbody></table>
