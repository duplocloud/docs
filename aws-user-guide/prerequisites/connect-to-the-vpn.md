# Connect to the VPN

DuploCloud integrates natively with OpenVPN by provisioning VPN users added in the Duplocloud portal. As a DuploCloud user, you can access resources in the private network by connecting to the VPN with the OpenVPN client.

{% hint style="info" %}
The OpenVPN Access Server is set to forward only traffic destined for network resources in the DuploCloud-managed private networks. Traffic accessing other resources on the internet does not pass through the tunnel.
{% endhint %}

## Obtain VPN Credentials

You can find your VPN credentials in the DuploCloud Portal on your user profile page. It can be accessed by clicking **Profile** in the user menu on the upper right of the page or through the **User** menu option on the left.&#x20;

<div align="left">

<figure><img src="../../.gitbook/assets/image (5) (5).png" alt=""><figcaption><p>User menu accessible from the user icon in the upper right</p></figcaption></figure>

</div>



<div align="left">

<figure><img src="../../.gitbook/assets/image (4) (4).png" alt=""><figcaption><p>VPN Details section of the user profile</p></figcaption></figure>

</div>

## Set up the OpenVPN User Profile and Client App

1. Click on the **VPN URL** link in the **VPN Details** section of your user profile.\
   \
   Modern browsers will call the link unsafe since it is using a self-signed certificate. Make the necessary selections to proceed anyway.
2. Log in to the OpenVPN Access Server user portal using the Username and Password from the **VPN Details** section of your DuploCloud user profile page.\
   \
   ![](<../../.gitbook/assets/image (10) (3).png>)
3. Click on the icon labeled **OpenVPN Connect Recommended for your device** to install the OpenVPN Connect app for your local machine.\
   \
   ![](<../../.gitbook/assets/image (8) (2).png>)
4. Navigate to your downloads folder, open the OpenVPN Connect file you downloaded in the previous step, and follow the prompts to finish the installation.&#x20;
5. In the **OpenVPN access server** dialog box, click on the blue **Yourself (user-locked profile)** link to download your OpenVPN user profile.
6. Navigate to your **Downloads** folder and click on the **.ovpn** file downloaded in the previous step. The **Onboarding Tour** dialog box displays.&#x20;
7. In the **Onboarding Tour** dialog box, click the **>** button twice. Click **Agree** and **OK** as needed to proceed to the **Import .ovpn profile dialog box**, and click **OK**. \
   \
   ![](<../../.gitbook/assets/image (2) (5).png>)
8. Click **OK**, and select **Connect after import**. Click **Add** in the upper right. If prompted to enter a password, use the password in the **VPN Profile** area of your user profile page in the DuploCloud Portal. You are now connected to the VPN.&#x20;
