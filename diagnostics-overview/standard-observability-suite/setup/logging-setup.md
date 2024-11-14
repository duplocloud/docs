---
description: Setting up Logging in the DuploCloud Portal
---

# Logging Setup

Navigate to **Administrator** -> **Observability** -> **Basic** -> **Settings**, and select the **Logging** tab to enable Logging. Click on **Enable Logging**. \


<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Enabling Standard Logging Stack</p></figcaption></figure>

The logging control plane is based on OpenSearch and Kibana, which are deployed in the Default tenant and configurable, as shown below.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

After enabling the control plane, choose which Tenants to collect logs from. The platform deploys collectors for each Tenant that you enable. Filebeat is the collector for Logs.

<figure><img src="../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p><strong>Logging</strong> tab for adding and enabling Tenant log collection</p></figcaption></figure>

{% hint style="warning" %}
If you have a multi-region setup, create a separate log setup for each region to avoid the cost of cross-region data transfer.
{% endhint %}
