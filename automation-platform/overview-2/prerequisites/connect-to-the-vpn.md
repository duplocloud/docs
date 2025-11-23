---
description: Connect to the DuploCloud VPN with the OpenVPN client
---

# Connect to the VPN

DuploCloud integrates with OpenVPN by provisioning VPN users added to the DuploCloud Portal. As a DuploCloud user, you can access resources in the private network by connecting to the VPN with the OpenVPN client.

{% hint style="info" %}
The **OpenVPN Access Server** forwards traffic only to network resources within the DuploCloud-managed private networks. Any traffic intended for other resources on the internet does not pass through the VPN tunnel.
{% endhint %}

## Obtaining VPN Credentials

User VPN credentials are accessible through the user profile page.&#x20;

1.  In the DuploCloud Portal, navigate to **Administrator** -> **Users** and select your user name, or click on the person icon (<img src="../../../.gitbook/assets/Screenshot (347) (1).png" alt="" data-size="line">) in the upper-right corner, and select **Profile**.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/image (187).png" alt="" width="261"><figcaption><p>The User menu</p></figcaption></figure></div>
2. You will find your VPN credentials in the **VPN Details** section of your profile.

<div align="left"><figure><img src="../../../.gitbook/assets/PROFILE (1).png" alt="" width="563"><figcaption><p>VPN Details section of the user profile</p></figcaption></figure></div>

## Setting up the OpenVPN User Profile and Client App

1. Click on the person icon (<img src="../../../.gitbook/assets/Screenshot (347).png" alt="" data-size="line">) in the upper right, and select **Profile**.&#x20;
2. In the **VPN Details** section, click **VPN URL**. Your browser may flag the link as unsafe due to a self-signed certificate. Click **Proceed Anyway** to continue.
3. Log in to the **OpenVPN Access Server** user portal using the credentials from the DuploCloud user profile section.\
   \
   ![](<../../../.gitbook/assets/image (31).png>)
4. Install the OpenVPN Connect app on your local machine.\
   \
   ![](<../../../.gitbook/assets/image (73).png>)
5. From the OpenVPN Access Server user portal, download your **user-locked profile** by clicking on the link labeled **Yourself** (this will generate the `.ovpn` file).\
   \
   ![](<../../../.gitbook/assets/image (202).png>)
6. Open the `.ovpn` file and click **OK** in the **Import .ovpn profile** dialog box.&#x20;
7. Once the profile is imported, click **Connect** to establish the VPN connection.\
   \
   ![](<../../../.gitbook/assets/image (47).png>)

