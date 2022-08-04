# VPN Setup

DuploCloud integrates natively with OpenVPN by provisioning VPN users added in the Duplocloud portal. OpenVPN setup is a two step process.

* Accepting Open VPN Free tier (Bring your own license) in AWS market place: Login to your AWS account console and go to this link [https://aws.amazon.com/marketplace/pp?sku=f2ew2wrz425a1jagnifd02u5t](https://aws.amazon.com/marketplace/pp?sku=f2ew2wrz425a1jagnifd02u5t) and accept the agreement. This adds no additional license cost other than the regular EC2 instance cost.
* Now go to DuploCloud Portal under Administrator --> System Settings --> VPN and click on Provision VPN. Soon the OpenVPN will be provisioned and be ready. Behind the scenes DuploCloud launches a cloud formation script to provision the OpenVPN.&#x20;

&#x20; &#x20;

![](<../../.gitbook/assets/image (2) (2).png>)

{% hint style="info" %}
You can find the OpenVPN admin password in the cloud formation stack in your AWS console.
{% endhint %}

Once the setup has been done, then while adding a user you can choose to provision a VPN for the user as shown in the screen below

![](<../../.gitbook/assets/image (7) (1).png>)

Users connected to VPN by default can SSH or RDP into EC2 instances and connect to internal load balancers and endpoints of the applications. However, in order to connect to other services like databases and elastic cache, you need to open that port to VPN under Administrator --> Tenant --> select the tenant and add a rule and choose the source as IP address and IP CIDR as VPN as shown below

![](<../../.gitbook/assets/image (3) (1).png>)
