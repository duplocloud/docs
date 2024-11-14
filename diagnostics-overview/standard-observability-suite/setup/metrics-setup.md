# Metrics Setup

The control plane for metrics is Grafana, Promethues and Yace. They are only deployable in Default tenant.&#x20;

Navigate to **Administrator** -> **Observability** -> **Basic** -> **Settings**, and select the **Monitoring** tab to enable Metrics. Click on **Enable Monitoring**.&#x20;

<div align="center">

<img src="../../../.gitbook/assets/mon_not_en (1).png" alt="Metrics Enable Monitoring link">

</div>

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

Following is how it looks after metrics control plane is operational. Cadvisor and Node Exporter are the collectors for metrics. Toggling one of the tenants shown in the picture below will deploy these containers on all the hosts in that tenant.

<figure><img src="../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>
