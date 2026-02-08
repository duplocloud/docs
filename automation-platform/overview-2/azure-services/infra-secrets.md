---
description: Create Infra Secrets to use with DuploCloud
---

# Infra Secrets

Infra Secrets in DuploCloud are used to securely store sensitive information, such as API keys, client secrets, or connection strings, needed for your infrastructure and application configurations. These secrets are managed within DuploCloud and can be used for secure access to services and resources. Infra Secrets provide a way to keep your sensitive data safe while allowing seamless integration with various DuploCloud services.

## Adding an Infra Secret

1. In the DuploCloud Portal, navigate to **Cloud Settings** → **Key Vault**.
2. Select the **Infra Secrets** tab.
3.  Click **Add**. The **Add Infra Secret** pane displays. <br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (375).png" alt="" width="327"><figcaption><p>The <strong>Add Infra Secret</strong> pane</p></figcaption></figure></div>
4. Complete the fields:

<table data-header-hidden><thead><tr><th width="117.11114501953125"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter the name of the Infra Secret. DuploCloud suggests using the Tenant name as a prefix.</td></tr><tr><td><strong>Value</strong></td><td>Enter the secret value (e.g., API key, client secret, connection string). This will be securely stored and used by DuploCloud services.</td></tr><tr><td><strong>Type</strong></td><td>Specify the type of secret, such as <code>API Key</code>, <code>Client Secret</code>, or <code>Connection</code>.</td></tr></tbody></table>

4. Click **Save** to store the Infra Secret securely.
