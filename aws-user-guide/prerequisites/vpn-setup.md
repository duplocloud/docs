---
description: Integrate with OpenVPN by provisioning VPN users
---

# VPN Setup

DuploCloud integrates natively with OpenVPN by provisioning VPN users that you add to the Duplocloud Portal. OpenVPN setup is a two-step process.

## Accept OpenVPN

Accept OpenVPN Free tier (Bring Your Own License) in the AWS marketplace:&#x20;

1. Log into your AWS account. In the console, navigate to: [https://aws.amazon.com/marketplace/pp?sku=f2ew2wrz425a1jagnifd02u5t](https://aws.amazon.com/marketplace/pp?sku=f2ew2wrz425a1jagnifd02u5t).&#x20;
2. Accept the agreement. Other than the regular EC2 instance cost, no additional license cost is added.

## Provision the VPN

1. In the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Click the **VPN** tab.
3. Click **Provision VPN.**

After the OpenVPN is provisioned, it is ready to use. Behind the scenes, DuploCloud launches a CloudFormation script to provision the OpenVPN.   &#x20;

![VPN tab in the System Settings page.](<../../.gitbook/assets/image (2) (2) (1).png>)

{% hint style="info" %}
You can find the OpenVPN admin password in the CloudFormation stack in your AWS console.
{% endhint %}

## **Provision the VPN and create a user**

Provision a VPN while creating a user:

1. In the DuploCloud Portal, navigate to **Administrator** -> **Users**.
2. Click **Add**. The **Create User** pane displays.
3. Enter a valid email address in the **Username** field.
4. In the **Roles** field, select the appropriate role for the User.
5. Select **Provision VPN**.
6. Click **Submit**.

<div align="left">

<figure><img src="../../.gitbook/assets/VPN_Create_User.png" alt=""><figcaption><p><strong>Create User</strong> pane</p></figcaption></figure>

</div>

### Deleting VPN access for a user

For information about removing VPN access for a user, see [Deleting a VPN user](../../user-administration-1/access-control/add-and-delete-vpn-access-for-users.md#deleting-a-vpn-user). To delete VPN access, you must have administrator privileges.&#x20;

## Open a VPN port

By default, users connected to a VPN can SSH or RDP into EC2 instances. Users can also connect to internal load balancers and endpoints of the applications. However, to connect to other services, such as databases and ElastiCache, you must open the port to the VPN:&#x20;

1. In the DuploCloud Portal, navigate to **Administrator** -> **Tenants**.
2. Select the Tenant in the **Name** column.
3. Click the **Security** tab.
4. Click **Add**. The Add Tenant Security pane displays.
5. In the **Source Type** field, select **Ip Address**.&#x20;
6. In the **IP CIDR** field, enter the name of your VPN.
7. Click **Add**.

<div align="left">

<figure><img src="../../.gitbook/assets/Add_Tenant_Security.png" alt=""><figcaption><p><strong>Add Tenant Security</strong> pane</p></figcaption></figure>

</div>
