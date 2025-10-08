---
description: Use KMS keys for resource encryption
---

# KMS Keys

DuploCloud allows you to configure Tenant and Plan level KMS (Key Management Service) keys for AWS/Azure resources. These keys can be selected when creating supported resources to ensure consistent encryption and help meet compliance requirements.

## Adding a KMS Key for a Plan

Plan-level KMS keys can be used for encrypting resources in any Tenant under the selected Plan.

1. Navigate to **Administrator** -> **Plans**.
2. Select the Plan from the **NAME** column.
3. Select the **KMS** tab.
4.  Click **Add**. The **Add a Kms Key** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (938).png" alt="" width="410"><figcaption><p><strong>Add a Kms Key</strong> pane </p></figcaption></figure></div>
5. Complete the following fields:

<table data-header-hidden><thead><tr><th width="177.55548095703125">Field</th><th>User Action / What to Enter</th></tr></thead><tbody><tr><td><strong>Key Name</strong></td><td>Enter a friendly name for the key (e.g., <code>test-key</code>)</td></tr><tr><td><strong>Key Id</strong></td><td>Enter the cloud provider–specific key ID (AWS KMS Key ID or Azure Key Vault Key ID).</td></tr><tr><td><strong>Key Arn</strong></td><td>Enter the cloud provider–specific key ARN or resource ID. For AWS this is the KMS Key ARN; for Azure, this is the Key Vault Key ID URI.</td></tr></tbody></table>

6. Click **Submit** to add the key to the Plan. Once added, the key can be selected when creating supported resources in the Plan, such as databases, compute instances, storage resources, and other services.

<figure><img src="../../../.gitbook/assets/Screenshot (941).png" alt=""><figcaption><p>Plan <strong>KMS</strong> tab in the DuploCloud Portal</p></figcaption></figure>

## Adding a KMS Key for a Tenant

Tenant-level KMS keys can be used for encrypting resources only within the selected tenant.

1. Navigate to **Administrator** -> **Tenants**.
2. Select the Tenant from the **NAME** column.
3. Select the **KMS** tab.
4.  Click **Add**. The **Add a Kms Key** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (937).png" alt="" width="410"><figcaption><p><strong>Add a Kms Key</strong> pane</p></figcaption></figure></div>
5. Complete the following fields:

<table data-header-hidden><thead><tr><th width="177.55548095703125">Field</th><th>User Action / What to Enter</th></tr></thead><tbody><tr><td><strong>Key Name</strong></td><td>Enter a friendly name for the key (e.g., <code>test-key</code>)</td></tr><tr><td><strong>Key Id</strong></td><td>Enter the cloud provider–specific key ID (AWS KMS Key ID or Azure Key Vault Key ID).</td></tr><tr><td><strong>Key Arn</strong></td><td>Enter the cloud provider–specific key ARN or resource ID. For AWS this is the KMS Key ARN; for Azure, this is the Key Vault Key ID URI.</td></tr></tbody></table>

6. Click **Submit** to add the key to the Tenant. Once added, the key can be selected when creating supported resources in the Tenant.

<figure><img src="../../../.gitbook/assets/Screenshot (940).png" alt=""><figcaption><p>Tenant <strong>KMS</strong> tab in the DuploCloud Portal</p></figcaption></figure>

## Selecting a KMS Key When Creating Resources

When creating a Host, RDS database, or other supported resource, select a KMS key to use for encrypting data at rest.&#x20;

1. Navigate to the resource creation page (e.g., **Hosts**, **RDS**, or other supported resources).
2. Locate the **Encryption Key** or **KMS Key** field.
3.  Choose a key from the options listed under **Default Tenant Key**, **Plan-level Keys**, or **Tenant-level Keys**.\


    <figure><img src="../../../.gitbook/assets/Screenshot (939).png" alt=""><figcaption><p><strong>Encryption Key</strong> selection options </p></figcaption></figure>
4. Complete the rest of the resource creation steps as usual.

{% hint style="info" %}
**Note:** Only applicable resources will display these key options. Unsupported resources will continue to use the default tenant key.
{% endhint %}
