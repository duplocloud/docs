# Metrics Setup

The metrics setup is made up of two components:

**Control Plane:** This comprises a Grafana dashboard service and a Prometheus container for fetching VM and container metrics. Grafana directly pulls cloud service metrics from AWS without requiring Prometheus.&#x20;

&#x20;From the DuploCloud Portal, navigate to **Administrator** -> **Observability** -> **Settings**, and select the **Monitoring** tab to enable Metrics. Click on **Enable Monitoring**.&#x20;

![](<../../.gitbook/assets/image (21) (1).png>)

**Metrics Collector**: Once Metrics control plane is ready i.e. Grafana and Prometheus service has been deployed and are active, we have to enable Metrics on a per-Tenant basis. From the DuploCloud portal, navigate to **Administrator** -> **Observability** -> **Settings**. Click the **Monitoring** tab and enable monitoring per Tenant using the toggle buttons. This triggers the deployment of Node Exporter and CAdvvisor container in each Host in the Tenant similar to how Log Collectors like File beat were deployed for fetching central logs and sending to Open Search.&#x20;
