---
description: Create, edit, view, or delete users and assign appropriate roles
---

# User Access to DuploCloud

{% hint style="warning" %}
You must be an Administrator to add, edit, or delete user access. If your User Source is Okta or Azure, add and remove users in the source system, not in DuploCloud.
{% endhint %}

## Adding a New User

Add a new user and give them appropriate permissions:&#x20;

1. In the DuploCloud Portal, navigate to **Administrator** -> **Users**.&#x20;
2.  Click **Add**. The **Create User** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (1136).png" alt="" width="452"><figcaption><p><strong>Create User</strong> pane</p></figcaption></figure></div>
3. In the **Username** field, enter the email or service account name. A service account is a special account used by an application, compute workload, or CI/CD tool, rather than a person. A username must be an email to match up to the SSO to access the web portal.&#x20;
4. Select a **Role**, then assign one or more **Tenants**, **Permissions Groups**, and **Permission Sets**.
5. If needed, select **Provision VPN** access and/or **Read Only Access**.
6. Click **Submit**.

## Editing Permissions for an Existing User

Edit an existing user's permissions and role:

1. In the DuploCloud Portal, navigate to **Administrator** -> **Users**.&#x20;
2. From the **USERNAME** column, select the user whose permissions you want to modify.
3. Click **Actions**, and select **Update**.&#x20;
4. Modify the user permissions as needed.
5. Click **Submit**.&#x20;

## Viewing Users

View users and their permissions:

1. In the DuploCloud Portal, navigate to **Administrator** -> **Users**.&#x20;
2. From the **USERNAME** column, select the user that you want to view.
3. The user page displays information about [**Tenant Access**](tenant-access/), [**VPN** access](add-and-delete-vpn-access-for-users.md), and API [**Tokens**](../api-and-session-management/api-tokens.md).<br>

<figure><img src="../../../.gitbook/assets/Screenshot (237).png" alt=""><figcaption><p>User page with <strong>Tenant Access</strong>, <strong>VPN</strong>, <strong>DevSpace</strong>, and <strong>Token</strong> tabs</p></figcaption></figure>

{% hint style="info" %}
The **Last Login** card shows the date and time of the user's last login.
{% endhint %}

## **Enabling Email Notification for New Admin Users**

When a new admin user is created in DuploCloud, you can configure the system to send an email notification for added visibility. This is especially useful for auditing and compliance purposes.

To enable email notifications for new admin users:

1. Navigate to **Administrator** -> **System Settings** -> **System Config**.
2.  Click **Add**. The **Add Config** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (379).png" alt=""><figcaption><p><strong>Add Config</strong> pane</p></figcaption></figure></div>
3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="150.888916015625"></th><th></th></tr></thead><tbody><tr><td><strong>Config Type</strong></td><td>Select <strong>Flags</strong></td></tr><tr><td><strong>Key</strong></td><td>Select <strong>Enable new admin notification</strong></td></tr><tr><td><strong>Value</strong></td><td>Set to <code>true</code> to activate email notifications for new admin users.</td></tr></tbody></table>

4. Click **Submit**. When the flag is set to `true`, an email will be sent to configured recipients every time a new admin user is added.&#x20;

## Deleting an Existing User

Delete an existing user and their permissions. Users managed by external providers (e.g., Okta) cannot be deleted.&#x20;

1. In the DuploCloud Portal, navigate to **Administrator** -> **Users**.&#x20;
2. From the **USERNAME** column, select the user that you want to delete.
3. Click **Actions,** and select **Delete**.&#x20;
4. Review the confirmation message and click **Confirm** to permanently delete the user.
