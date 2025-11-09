---
description: Manage VPN access for users
---

# VPN access for users

{% hint style="warning" %}
To add or delete VPN access for users you must have **Administrator** privileges.&#x20;
{% endhint %}

## Adding VPN access for a user

Add a VPN connection for a user:

1. In the DuploCloud Portal, navigate to **Administrator** -> **Users**. The **Users** page displays.
2. Select the name of the user that will have VPN access.&#x20;
3. Click the **VPN** tab.&#x20;
4. Click **Set VPN**. The Set VPN pane displays.
5. Select the appropriate options, including **Reallocate VPN Address** and **Regenerate Password**.
6. Click **Create**.

<div align="left"><figure><img src="../../.gitbook/assets/Set_VPN.png" alt=""><figcaption><p><strong>Set VPN</strong> pane</p></figcaption></figure></div>

## Deleting a VPN user

To delete VPN access, you must have administrator privileges.&#x20;

Delete a user's VPN connection:

1. In the DuploCloud Portal, navigate to **Administrator** -> **Users**.
2. On the **Users** page, select the user name from the **Username** column.
3. Click the **VPN** tab.&#x20;
4. Click **Remove VPN** and **Confirm**.&#x20;

VPN access is removed for the user that you selected.

## **Managing VPN Access for Okta users**

Admins can choose to enable VPN access by default for new Okta users or require manual approval before granting access. Admin users can still update VPN settings for individual users as needed.

1. Navigate to **Administrator** -> **System Settings**.
2.  Select **System Config**, and click **Add**. The **Update Config AppConfig** pane displays. \


    <div align="left"><figure><img src="../../.gitbook/assets/image (8).png" alt="" width="343"><figcaption><p>The <strong>Update Config AppConfig</strong> pane</p></figcaption></figure></div>
3. In the **Config Type** list box, select **AppConfig**.&#x20;
4. In the **Key** field, enter `DisableOktaUsersVpnSync`.
5. In the **Value** field, enter **true** or **false**:
   * **true:** VPN access is disabled by default for new Okta users.
   * **false**: VPN access is enabled for new Okta users.
6. Click **Submit**. Okta users' VPN access is enabled or disabled.&#x20;

For more details about using Okta with DuploCloud, refer to [Okta Identity Management](sso-configuration/okta-identity-management.md).
