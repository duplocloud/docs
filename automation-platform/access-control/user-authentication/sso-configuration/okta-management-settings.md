---
description: Configure Okta management settings from the DuploCloud Portal
---

# Okta Management Settings

Okta is a cloud-based identity and access management platform that provides Single Sign-On (SSO), multi-factor authentication (MFA), and lifecycle management for users. DuploCloud supports Okta integration for authentication, authorization, and group-based access mapping.

This page describes the current, portal-based configuration for Okta. If you are migrating from legacy configuration files, DuploCloud automatically migrates existing settings to the portal. (merged from first page).

Initial setup may require coordination with the DuploCloud support team.

## Configuring Okta Settings

Configure your Okta integration settings from directly within the DuploCloud Portal:

1. Log in to the DuploCloud Portal as an administrator.
2. Navigate to **Administrator** → **System Settings**.
3.  Select the **Okta Settings** tab. The **Okta Settings** pane displays.<br>

    <figure><img src="../../../../.gitbook/assets/Screenshot (665).png" alt=""><figcaption><p><strong>Okta Settings</strong> pane</p></figcaption></figure>
4. Configure the desired fields in the following sections:

### **User Source Settings**

<table data-header-hidden><thead><tr><th width="279.99993896484375">Field</th><th width="494.333251953125">Description</th></tr></thead><tbody><tr><td><strong>Enable Okta As User Source</strong></td><td>Select this option to make Okta the primary source for user identities in DuploCloud.</td></tr><tr><td><strong>DuploCloud Admin Group ID*</strong></td><td>Enter the Okta Group ID that grants administrator access to users within DuploCloud. You can find the Okta Group ID by navigating to <strong>Directory</strong> → <strong>Groups</strong> in Okta, selecting the desired group, and copying the <strong>Group ID</strong> from the <strong>General</strong> tab. </td></tr><tr><td><strong>DuploCloud ReadOnly Group ID</strong></td><td>Specify the Okta Group ID for users who should have read-only access permissions. To find the DuploCloud ReadOnly Group ID, navigate to <strong>Directory</strong> → <strong>Groups</strong> in Okta, select the read-only group, and copy he <strong>Group ID</strong> from the <strong>General</strong> tab. This ID grants read-only access to users in DuploCloud.</td></tr><tr><td><strong>DuploCloud Security Group ID</strong></td><td>Provide the Okta Group ID assigned to security-focused roles or permissions in DuploCloud. To find the DuploCloud Security Group IP, navigate to <strong>Directory → Groups</strong> in Okta, select the security group, and copy the <strong>Group ID</strong> from the <strong>General</strong> tab.</td></tr><tr><td><strong>DuploCloud Tenant Group Prefix</strong></td><td>Specify the prefix used for Okta groups that map to DuploCloud tenants. For example, if your tenant groups are named <code>tenant1-admin</code> and <code>tenant2-admin</code>, the prefix would be <code>tenant-</code>.</td></tr><tr><td><strong>DuploCloud Tenant ReadOnly Group Prefix</strong></td><td>Specify the prefix for Okta groups that have read-only access within DuploCloud Tenants. For example, if your read-only groups are named <code>readonly-team1</code> and <code>readonly-team2</code>, the prefix would be <code>readonly-</code>.</td></tr></tbody></table>

### **Okta API Token Settings**

<table data-header-hidden><thead><tr><th width="259.333251953125">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Okta API Token*</strong></td><td>Enter the API token used by DuploCloud to synchronize users and groups with Okta.</td></tr><tr><td><strong>Okta API Token ID*</strong></td><td>Enter the identifier for the currently active Okta API token.</td></tr><tr><td><strong>Admin Email*</strong></td><td>Provide the email address that will receive notifications related to API token expiration and other Okta alerts.</td></tr></tbody></table>

{% hint style="info" %}
DuploCloud displays the current Okta API token’s expiration date and shows alerts if it is expired or near expiration.&#x20;
{% endhint %}

### **Single Sign-On Settings**

<table data-header-hidden><thead><tr><th width="254">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Enable Okta Login*</strong></td><td>Select this option to enable Okta Single Sign-On (SSO) for user login in DuploCloud.</td></tr><tr><td><strong>Okta Domain*</strong></td><td>Enter your Okta organization's domain URL (e.g., <code>https://dev-32616951.okta.com</code>).</td></tr><tr><td><strong>Client ID*</strong></td><td>Enter the OAuth 2.0 Client ID from your Okta application.</td></tr><tr><td><strong>Client Secret*</strong></td><td>Enter the OAuth 2.0 Client Secret associated with your Okta Client ID.</td></tr><tr><td><strong>Enable DPoP</strong></td><td>Enable this option to activate Demonstration of Proof of Possession (DPoP) for enhanced OAuth security.</td></tr></tbody></table>

5. Click **Save** to apply your changes.

## Managing Okta Users, Permissions, and API Tokens

Once the initial integration is setup and fully configured, you can use the [Okta Portal](https://login.okta.com/) to add users, assign roles and permissions, delete users, revoke permissions, and generate and manage Okta API tokens. See the Okta documentation for specific tasks:

### **Manage Okta Users**

* [Add Okta users](https://help.okta.com/en-us/content/topics/users-groups-profiles/usgp-people.htm?cshid=ext_Directory_People)
* [Manage users](https://help.okta.com/en-us/content/topics/users-groups-profiles/usgp-people.htm?cshid=ext_Directory_People)
* [Delete a user](https://help.okta.com/oie/en-us/content/topics/users-groups-profiles/usgp-deactivate-user-account.htm)

### **Assign Roles and Permissions**

* [Manage administrative roles](https://help.okta.com/en-us/content/topics/security/administrators-set-up-admins.htm)
* [Assign a role to a user](https://help.okta.com/wf/en-us/content/topics/workflows/connector-reference/azuread/actions/assignroletouser.htm)

### **Revoke Permissions:**

* [Remove or change an admin role](https://help.okta.com/oie/en-us/content/topics/security/admin-remove-assignment.htm)
* [Disable VPN Access for Okta users](../../user-access-and-permissions/add-and-delete-vpn-access-for-users.md#managing-vpn-access-for-okta-users)

### **Generate and Manage Okta API Tokens:**

* [Create an Okta API token](https://help.okta.com/en-us/content/topics/security/api.htm#create-okta-api-token)
* [Manage Okta API tokens](https://help.okta.com/en-us/content/topics/security/api.htm)

{% hint style="info" %}
**Synching updates**: It can take several minutes for changes made in Okta to reflect in the DuploCloud UI. To force immediate synchronization:

* Navigate to **Administrator** → **Users** in DuploCloud, and click **Sync**.
{% endhint %}
