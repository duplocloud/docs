# Metrics Setup

Metrics setup comprises of two parts

**Control Plane:** This comprises of a Grafana service for dashboard and a Prometheus container for fetching VM and container metrics. Cloud service metrics are directly pulled by Grafana from AWS without requiring Prometheus.&#x20;

&#x20;To enable Metrics, from the DuploCloud Portal, navigate to **Administrator** -> **Observability** -> **Settings**, and select the **Monitoring** tab. Click on **Enable Monitorin**g.&#x20;

![](<../../.gitbook/assets/image (21) (1).png>)

**Metrics Collector**: Once Metrics control plane is ready i.e. Grafana and Prometheus service has been deployed and are active, we have to enable Metrics on a per-Tenant basis. From the DuploCloud portal, navigate to **Administrator** -> **Observability** -> **Settings**. Click the **Monitoring** tab and enable monitoring per Tenant using the toggle buttons. This triggers the deployment of Node Exporter and CAdvvisor container in each Host in the Tenant similar to how Log Collectors like File beat were deployed for fetching central logs and sending to Open Search.&#x20;
