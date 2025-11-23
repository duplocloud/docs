---
description: Create and manage Google Cloud secrets in DuploCloud
---

# GCP Secrets Manager

DuploCloud integrates with **GCP Secrets Manager** to help you securely store and manage sensitive information such as API keys, credentials, and tokens. Secrets can be created and managed directly from the DuploCloud Portal and are automatically provisioned to your GCP environment, inheriting GCP’s native encryption and access control policies.

## Adding a Secret

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Secrets**.
2.  Click **Add**. The **Add Google Secret** pane displays.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (518).png" alt=""><figcaption><p><strong>Add Google Secret</strong> pane in the DuploCloud Portal</p></figcaption></figure>
3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="224.6666259765625">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Provide a name for the secret which will be the identifier in DuploCloud and GCP.</td></tr><tr><td><strong>Secret Value Type</strong></td><td>Select the secret format (<strong>String</strong> or <strong>JSON</strong>).</td></tr><tr><td><strong>Secret Value</strong></td><td>Enter the actual secret you want to store securely.</td></tr><tr><td><strong>Labels</strong></td><td>Enter optional key-value pairs to help categorize or manage the secret.</td></tr><tr><td><strong>Replication Type</strong></td><td>Choose how GCP replicates the secret: <strong>Automatic</strong> (managed by Google) or <strong>User Managed</strong> (you specify the regions).</td></tr></tbody></table>

4.  Click **Submit** to create the secret. The secret is created in CGP Secrets Manager and displays on the **Secrets** page in the DuploCloud Portal.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (519).png" alt=""><figcaption><p><strong>Secrets</strong> page in the DuploCloud Portal</p></figcaption></figure>

## Viewing Secrets

After creating a secret, view its details directly from the DuploCloud Portal.

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Secrets.**
2. Click on the secret name in the **NAME** column to open the details page.&#x20;
3. Select the **Details** or **YAML** tab to review the secret's metadata, value, labels, and configuration.

<figure><img src="../../../.gitbook/assets/Screenshot (521).png" alt=""><figcaption><p><strong>Details</strong> tab for the <code>app-secret</code> secret</p></figcaption></figure>

{% hint style="info" %}
Secret values may be masked depending on your access level.
{% endhint %}

## Managing Secrets

View, update, or delete existing secrets using the actions menu in the DuploCloud Portal.

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Secrets**.
2.  Click the menu icon (<img src="../../../.gitbook/assets/menu icon (12).avif" alt="" data-size="line">) in the row of the secret you want to manage.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (520).png" alt=""><figcaption><p><strong>Secrets</strong> page with menu options highlighted</p></figcaption></figure>
3. Choose from the available actions:

<table data-header-hidden><thead><tr><th width="148.22216796875">Action</th><th>Description</th></tr></thead><tbody><tr><td><strong>View</strong></td><td>Open the secret’s data and metadata in JSON format.</td></tr><tr><td><strong>Update</strong></td><td>Modify the secret’s value or labels.</td></tr><tr><td><strong>Delete</strong></td><td>Permanently remove the secret.</td></tr></tbody></table>
