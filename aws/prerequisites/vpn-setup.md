---
description: Integrate with OpenVPN by provisioning VPN users
---

# VPN Setup

DuploCloud integrates natively with OpenVPN by provisioning VPN users added to the Duplocloud Portal. OpenVPN setup is a two-step process.

## Accept OpenVPN

Accept OpenVPN Free tier (Bring your own license) in the AWS marketplace:&#x20;

1. &#x20;Log into your AWS account. In the console, navigate to: [https://aws.amazon.com/marketplace/pp?sku=f2ew2wrz425a1jagnifd02u5t](https://aws.amazon.com/marketplace/pp?sku=f2ew2wrz425a1jagnifd02u5t).&#x20;
2. Accept the agreement. No additional license cost, other than the regular EC2 instance cost, is added.

## Provision the VPN

In the DuploCloud Portal:

1. Navigate to **Administrator** --> **System Settings**.
2. Click the **VPN** tab.
3. Click **Provision VPN.**

The OpenVPN will be provisioned and ready shortly. Behind the scenes, DuploCloud launches a cloud formation script to provision the OpenVPN.   &#x20;

![VPN tab in the System Settings page.](<../../.gitbook/assets/image (2) (2) (1).png>)

{% hint style="info" %}
You can find the OpenVPN admin password in the cloud formation stack in your AWS console.
{% endhint %}

## **Provision the VPN and create a user**

You provision a VPN while creating a user:

1. In the DuploCloud Portal, navigate to **Administrator** -> **Users**.
2. Click **Add**. The **Create User** pane displays.
3. Enter a valid email address in the **Username** field.
4. In the **Roles** field select the appropriate role for the User.
5. Select **Provision VPN**.
6. Click **Submit**.

![Create User pane](<../../.gitbook/assets/image (7) (2).png>)

## Open a VPN port

Users connected to a VPN by default can SSH or RDP into EC2 instances. Users can also connect to internal load balancers and endpoints of the applications. However, In order to connect to other services, such as databases and elastic cache, you must open the port to the VPN:&#x20;

1. In the DuploCloud Portal, navigate to **Administrator** --> **Tenant**.
2. Select the Tenant in the **Name** column.
3. Click the **Security** tab.
4. Click **Add**. The Add Tenant Security pane displays.
5. In the **Source Type** field, select **Ip Address**.&#x20;
6. In the **IP CIDR** field, enter the name of your VPN.
7. Click **Add**.

![Add Tenant Security pane](<../../.gitbook/assets/image (3) (3).png>)
