---
description: Grant tenant-specific access to resources over a VPN
---

# Tenant Security Rules for VPN Access

For DuploCloud users to access internal resources in a Tenant, such as Hosts or databases, you must add security rules to allow a VPN connection. For details on VPN user access, see [VPN Access for Users](../../access-control/user-access-and-permissions/add-and-delete-vpn-access-for-users.md).

{% hint style="info" %}
**Note:** Administrators have persistent access to all Tenants and do not need to add individual Tenant access for themselves.
{% endhint %}

## Adding Tenant Security Rules for a VPN

To define tenant security rules for VPN access:

1. In the DuploCloud Portal, navigate to **Administrators** -> **Tenants.**
2. Select the Tenant in the **NAME** column.
3. Click the **Security** tab.&#x20;
4.  Click **Add**. The **Add Tenant Security** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screen Shot 2023-01-26 at 5.47.52 PM.png" alt=""><figcaption><p><strong>Add Tenant Security</strong> pane</p></figcaption></figure></div>
5. Complete the fields to configure the security rule.&#x20;
   * In the example shown, the rule allows traffic originating from the VPN IP address to access resources that are private or internal to the tenant.
6. Click **Add** to save the rule.&#x20;

{% hint style="info" %}
If you want to grant some VPN users access while excluding others, add a separate security rule for each user using their individual IP address.
{% endhint %}
