---
description: Enable Metrics for the DuploCloud Portal
---

# Metrics Setup

The metrics setup is made up of two components:

**Control Plane** comprises a Grafana dashboard service and a Prometheus container for fetching VM and container metrics. Grafana directly pulls cloud service metrics from AWS without requiring Prometheus.&#x20;

&#x20;From the DuploCloud Portal, navigate to **Administrator** -> **Observability** -> **Basic** -> **Settings**, and select the **Monitoring** tab to enable Metrics. Click on **Enable Monitoring**.&#x20;

<div align="center">

<img src="../../../.gitbook/assets/mon_not_en (1).png" alt="Metrics Enable Monitoring link">

</div>

**Metrics Collector.** Once the Metrics control plane is ready, i.e., Grafana and Prometheus service has been deployed and are active, we have to enable Metrics on a per-Tenant basis. From the DuploCloud portal, navigate to **Administrator** -> **Observability** -> **Basic** -> **Settings**. Click the **Monitoring** tab and enable monitoring per Tenant using the toggle buttons. This triggers the deployment of Node Exporter and CAdvisor container in each Host in the Tenant, similar to how Log Collectors like Filebeat are deployed for fetching central logs and sending them to Open Search.&#x20;
