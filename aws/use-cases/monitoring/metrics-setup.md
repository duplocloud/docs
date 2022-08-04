# Metrics Setup

Metrics setup comprises of two parts

**Control Plane:** This comprises of a Grafana service for dashboard and a Prometheus container for fetching VM and container metrics. Cloud service metrics are directly pulled by Grafana from AWS without requiring Prometheus.&#x20;

&#x20;To enable Metrics go under Administrator --> Diagnostics --> Settings --> Monitoring and click on "Enable Monitoring"&#x20;

![](<../../../.gitbook/assets/image (21) (1) (2).png>)

**Metrics Collector**: Once Metrics control plane is ready i.e. Grafana and Prometheus service has been deployed and are active, we have to enable Metrics on a per tenant basis from Admin-->Diagnostics -> Settings --> Monitoring by enabled the per tenant toggle button. This triggers the deployment of Node Exporter and CAdvvisor container in each host in the tenant similar to how Log Collectors like File beat were deployed for fetching central logs and sending to Open Search.&#x20;
