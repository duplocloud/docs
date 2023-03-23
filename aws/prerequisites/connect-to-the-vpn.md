# Connect to the VPN

DuploCloud integrates natively with OpenVPN by provisioning VPN users added in the Duplocloud portal. As a DuploCloud user, you can access resources in the private network by connecting to the VPN with the OpenVPN client.

{% hint style="info" %}
The OpenVPN Access Server is set to forward only traffic destined for network resources in the DuploCloud-managed private networks. Traffic accessing other resources on the internet does not pass through the tunnel.
{% endhint %}

## Obtain VPN Credentials

User VPN credentials are accessible on the user profile page. It can be accessed through the menu on the upper right of the page or through the User menu option on the left.&#x20;

<figure><img src="../../.gitbook/assets/image (5) (5).png" alt=""><figcaption><p>User menu accessible from the user icon in the upper right</p></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (4) (4).png" alt=""><figcaption><p>VPN Details section of the user profile</p></figcaption></figure>

## Set up the OpenVPN User Profile and Client App

1. Follow the VPN URL link in the VPN Details section of your user profile.\
   \
   Modern browsers will call the link unsafe since it is using a self-signed certificate. Proceed to it.
2. Log in to the OpenVPN Access Server user portal using the credentials from the DuploCloud user profile section.\
   \
   ![](<../../.gitbook/assets/image (10) (3).png>)
3. Install the OpenVPN Connect app for your local machine.\
   \
   ![](<../../.gitbook/assets/image (8) (2).png>)
4. Download the OpenVPN user profile for your account from the link labeled Yourself (user-locked profile).\
   \
   ![](<../../.gitbook/assets/image (3) (4).png>)
5. Open the .ovpn file and click OK at the Import profile dialog. Then click Connect.\
   \
   ![](<../../.gitbook/assets/image (2) (5).png>)

