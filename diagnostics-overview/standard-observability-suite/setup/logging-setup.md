# Logging Setup

Navigate to **Administrator** -> **Observability** -> **Basic** -> **Settings**, and select the **Logging** tab to enable Logging. Click on **Enable Logging**. \


<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Enabling Standard Logging Stack</p></figcaption></figure>

The control plane for logging is opensearch and Kibana which are deployed by default in the default tenant and is configurable as shown below.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

After enabling the control plane, the user can choose which tenants to collect logs from and based on what tenants are enabled, the platform will deploy the collectors in that tenant. File beat is the collector for Logs

<figure><img src="../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>



{% hint style="info" %}
If you have a multi-region setup then it is advisable that you have seprate logging setup for each region to avoid cross region data transfer cost
{% endhint %}
