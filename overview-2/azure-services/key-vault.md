---
description: Configure Azure Key Vault with DuploCloud for secure secret storage
---

# Key Vault

DuploCloud integrates with Azure Key Vault to secure the storage of secrets, such as passwords and database connection strings.

## Configuring Azure Key Vault

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Key Vault**.
2.  Click **Add**. The **Create a** **Key Vault** pane displays.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (72).png" alt=""><figcaption><p>The <strong>Create a</strong> <strong>Key Vault</strong> pane</p></figcaption></figure></div>
3. Enter a **Name** for the Key Vault.
4. Select a **SKU Pricing Tier**: **Standard** or **Premium**.
5. Optionally, enable **Purge Protection**. Once enabled, this cannot be reversed.
6. Specify the **Retention Days** for key vault items.
7. Click **Create** to provision the Key Vault.&#x20;

## Adding Secrets to Key Vault

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Key Vault**.
2. Select the **Azure Key Vaults** tab. &#x20;
3. Select the Key Vault from the **NAME** column.&#x20;
4. Select the **Secrets** tab.
5.  Click, **Add**. The **Create a Secret** pane displays. \


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (108).png" alt="" width="453"><figcaption><p>The <strong>Create a Secret</strong> pane</p></figcaption></figure></div>
6. Complete the following fields on the **Create a Secret** pane:
   * **Name**: Specify the name of the secret.
   * **Secret Value**: Enter the actual value of the secret.
   * **Content Type**: Define the type of content stored in the secret (e.g., `text/plain`, `application/json`).
7. Click **Submit**.&#x20;

## Updating a Secret in Azure Key Vault

After creating a Key Vault and adding secrets, you can update an existing secret when needed. Follow these steps to update a secret in your Azure Key Vault:

1. In the DuploCloud Portal, go to **Cloud Services** -> **Key Vault**.
2. Select the Key Vault you wish to manage from the **NAME** column.
3. Select the **Secrets** tab.
4. Click the menu icon (<img src="../../.gitbook/assets/menu icon (6).avif" alt="" data-size="line">) next to the secret you want to update.
5. From the menu options, select **Edit**. The **Update a Secret** pane displays.
6. Update the **Value** field with the new data you want to store.
7. Click **Update** to apply the changes. The updated secret will now be stored as a new version, and the old version will be moved to the secret's version history.

## **Versioning and Viewing Secret Versions**

To view secret versions, click the caret (<img src="../../.gitbook/assets/Screenshot (111).png" alt="" data-size="line">) next to a secret's name. A list of available versions will appear.

To view a specific version, click the menu icon (<img src="../../.gitbook/assets/menu icon (6).avif" alt="" data-size="line">) next to the version and select **View**. The **JSON representation** of that version displays.

<figure><img src="../../.gitbook/assets/Screenshot (110) (1).png" alt=""><figcaption></figcaption></figure>
