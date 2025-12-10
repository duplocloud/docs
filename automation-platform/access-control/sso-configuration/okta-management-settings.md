---
description: Configure Okta management settings from the DuploCloud Portal
---

# Okta Management Settings

DuploCloud has transitioned Okta management from legacy configuration files to a streamlined, self-service UI within the DuploCloud Portal. This change allows you to configure advanced Okta integration options such as enabling Okta as the primary user source, managing Single Sign-On parameters, and maintaining API tokens, all without manual file edits.

DuploCloud will automatically migrate your current Okta settings from the old `exe.config` file into the portal’s settings database. After migration, all Okta configuration changes should be made through this UI.

## Configuring Okta Settings

Configure your Okta integration settings from directly within the DuploCloud Portal:

1. Log in to the DuploCloud Portal as an administrator.
2. Navigate to **Administrator** → **System Settings**.
3.  Select the **Okta Settings** tab. The **Okta Settings** pane displays.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (665).png" alt=""><figcaption><p><strong>Okta Settings</strong> pane</p></figcaption></figure>
4. Configure the desired fields in the following sections:

### **User Source Settings**

<table data-header-hidden><thead><tr><th width="317.3333740234375">Field</th><th width="494.333251953125">Description</th></tr></thead><tbody><tr><td><strong>Enable Okta As User Source</strong></td><td>Select this option to make Okta the primary source for user identities in DuploCloud.</td></tr><tr><td><strong>DuploCloud Admin Group ID*</strong></td><td>Enter the Okta Group ID that grants administrator access to users within DuploCloud.</td></tr><tr><td><strong>DuploCloud ReadOnly Group ID</strong></td><td>Specify the Okta Group ID for users who should have read-only access permissions.</td></tr><tr><td><strong>DuploCloud Security Group ID</strong></td><td>Provide the Okta Group ID assigned to security-focused roles or permissions in DuploCloud.</td></tr><tr><td><strong>DuploCloud Sign Up Group ID</strong></td><td>Input the Okta Group ID for users allowed to self-register or onboard within DuploCloud.</td></tr><tr><td><strong>DuploCloud Tenant Group Prefix</strong></td><td>Define the prefix used to map Okta groups to specific DuploCloud Tenants.</td></tr><tr><td><strong>DuploCloud Tenant ReadOnly Group Prefix</strong></td><td>Set the prefix for Okta groups that have read-only access within DuploCloud Tenants.</td></tr></tbody></table>

### **Okta API Token Settings**

<table data-header-hidden><thead><tr><th width="259.333251953125">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Okta API Token*</strong></td><td>Enter the API token used by DuploCloud to synchronize users and groups with Okta.</td></tr><tr><td><strong>Okta API Token ID*</strong></td><td>Enter the identifier for the currently active Okta API token.</td></tr><tr><td><strong>Admin Email*</strong></td><td>Provide the email address that will receive notifications related to API token expiration and other Okta alerts.</td></tr></tbody></table>

{% hint style="info" %}
DuploCloud displays the current Okta API token’s expiration date and time in the **Okta API Token Settings** area. If the token is expired or nearing expiration, you will see an alert prompting you to update the token immediately.&#x20;
{% endhint %}

### **Single Sign-On Settings**

<table data-header-hidden><thead><tr><th width="254">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Enable Okta Login*</strong></td><td>Select this option to enable Okta Single Sign-On (SSO) for user login in DuploCloud.</td></tr><tr><td><strong>Okta Domain*</strong></td><td>Enter your Okta organization's domain URL (e.g., <code>https://dev-32616951.okta.com</code>).</td></tr><tr><td><strong>Client ID*</strong></td><td>Enter the OAuth 2.0 Client ID from your Okta application.</td></tr><tr><td><strong>Client Secret*</strong></td><td>Enter the OAuth 2.0 Client Secret associated with your Okta Client ID.</td></tr><tr><td><strong>Enable DPoP</strong></td><td>Enable this option to activate Demonstration of Proof of Possession (DPoP) for enhanced OAuth security.</td></tr></tbody></table>

5. Click **Save** to apply your changes.
