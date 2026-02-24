---
description: Manage VPN access for users
---

# VPN Access for Users

DuploCloud allows administrators to grant users secure access to tenant resources via a VPN.

{% hint style="warning" %}
**Note:** VPN features in DuploCloud are available only after the VPN service has been enabled for your Tenant. For instructions on enabling VPN, see the VPN setup page for your cloud provider:

* [AWS VPN Setup](../../overview/prerequisites/vpn-setup.md)
* [Azure VPN Setup](../../overview-2/prerequisites/connect-to-the-vpn.md)
* [GCP VPN Setup](../../overview-1/prerequisites/vpn/vpn-setup.md)
{% endhint %}

## Adding VPN Access for a User

1. Navigate to **Administrator** -> **Users**.&#x20;
2. Select the name of the user that will have VPN access.&#x20;
3. Click the **VPN** tab.&#x20;
4.  Click **Set VPN**. The **Set VPN** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Set_VPN.png" alt=""><figcaption><p><strong>Set VPN</strong> pane</p></figcaption></figure></div>
5. Select **Reallocate VPN Address** and/or **Regenerate Password**.
6. Click **Create**.

## Deleting a VPN User

1. Navigate to **Administrator** -> **Users**.
2. Select the user name from the **USERNAME** column.
3. Select the **VPN** tab.&#x20;
4. Click **Remove VPN** and **Confirm**.&#x20;

VPN access is removed for the selected user.

## Managing VPN Access for Okta Users

Admins can choose to enable VPN access by default for new Okta users or require manual approval before granting access. Admin users can still update VPN settings for individual users as needed.

1. Navigate to **Administrator** -> **System Settings**.
2.  Select **System Config**, and click **Add**. The **Update Config AppConfig** pane displays. <br>

    <div align="left"><figure><img src="../../../.gitbook/assets/image (8).png" alt="" width="343"><figcaption><p><strong>Update Config AppConfig</strong> pane</p></figcaption></figure></div>
3. In the **Config Type** list box, select **AppConfig**.&#x20;
4. In the **Key** field, enter `DisableOktaUsersVpnSync`.
5. In the **Value** field, enter `true` or `false`:
   * `true`**:** VPN access is disabled by default for new Okta users.
   * `false`: VPN access is enabled for new Okta users.
6. Click **Submit**. Okta users' VPN access is enabled or disabled.&#x20;

For more details about using Okta with DuploCloud, refer to [Okta Identity Management](/broken/pages/yeRYLkYWOI0ef3Tgwdd6).
