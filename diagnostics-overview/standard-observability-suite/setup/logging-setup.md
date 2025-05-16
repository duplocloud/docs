---
description: Setting up Logging in the DuploCloud Portal
---

# Logging Setup

Navigate to **Administrator** -> **Observability** -> **Standard** -> **Settings**, and select the **Logging** tab to enable Logging. Click on **Enable Logging**.&#x20;

<figure><img src="../../../.gitbook/assets/ENABLE LOGGING (1).png" alt=""><figcaption></figcaption></figure>

Logging is based on OpenSearch and Kibana, deployed in the Tenant of your choice, and configurable, as shown below.

<figure><img src="../../../.gitbook/assets/ENABLE LOGGING.png" alt=""><figcaption></figcaption></figure>

After enabling logging, choose which Tenants to collect logs from. The platform deploys collectors for each Tenant that you enable. Filebeat is the collector for Logs.

<figure><img src="../../../.gitbook/assets/Screenshot (112).png" alt=""><figcaption><p><strong>Logging</strong> tab for adding and enabling Tenant log collection</p></figcaption></figure>

{% hint style="warning" %}
If you have a multi-region setup, create a separate logging infrastructure setup for each region to avoid the cost of cross-region data transfer.
{% endhint %}
