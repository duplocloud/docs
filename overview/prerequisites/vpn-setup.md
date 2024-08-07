---
description: Accept OpenVPN, provision the VPN, and add VPN users
---

# VPN Setup

DuploCloud integrates with OpenVPN by provisioning VPN users that you add to the DuploCloud Portal. OpenVPN setup is a two-step process.

## Accepting OpenVPN

Accept OpenVPN Free Tier (Bring Your Own License) in the AWS Marketplace:&#x20;

1. Log into your AWS account. In the console, navigate to: [https://aws.amazon.com/marketplace/pp?sku=f2ew2wrz425a1jagnifd02u5t](https://aws.amazon.com/marketplace/pp?sku=f2ew2wrz425a1jagnifd02u5t).&#x20;
2. Accept the agreement. Other than the regular EC2 instance cost, no additional license costs are added.

## Provisioning the VPN

1. In the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Select the **VPN** tab.
3. Click **Provision VPN.**

After the OpenVPN is provisioned, it is ready to use. Behind the scenes, DuploCloud launches a CloudFormation script to provision the OpenVPN.   &#x20;

![The VPN tab on the System Settings page in the DuploCloud Portal](<../../.gitbook/assets/image (2) (2) (1).png>)

{% hint style="info" %}
You can find the OpenVPN admin password in the CloudFormation stack in your AWS console.
{% endhint %}

## Adding or Deleting a VPN User

For instructions to add or delete a VPN user, see the DuploCloud [User Administration documentation](../../access-control/add-and-delete-vpn-access-for-users.md).

## Opening a VPN Port

Users connected to a VPN can SSH or RDP into EC2 instances by default. Users can also connect to internal application Load Balancers and endpoints. However, to connect to other Services, such as databases and ElastiCache, you must open the port to the VPN:&#x20;

1. In the DuploCloud Portal, navigate to **Administrator** -> **Tenants**.
2. Select the Tenant from the **NAME** column.
3. Click the **Security** tab.
4. Click **Add**. The **Add Tenant Security** pane displays.
5. From the **Source Type** list box, select **IP Address**.&#x20;
6. From the **IP CIDR** list box, select your IP CIDR.
7. Click **Add**.

<div align="left">

<figure><img src="../../.gitbook/assets/Add_Tenant_Security.png" alt=""><figcaption><p>The <strong>Add Tenant Security</strong> pane</p></figcaption></figure>

</div>
