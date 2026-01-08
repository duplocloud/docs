---
description: Viewing Observability data using DuploCloud's Advanced Observability Suite
---

# Advanced Observability Suite (AOS)

DuploCloud's **Advanced Observability Suite (AOS)** is an add on observability service that provides dynamic, in-depth observability monitoring, including traces, profiling, alerts, and cross-Tenant analytics.&#x20;

{% hint style="info" %}
**Hint:** If you do not see the Advanced Observability Suite in your DuploCloud Portal, please contact DuploCloud Support to enable this add-on.
{% endhint %}

For daily operations using the default observability offering, see [Standard Observability](standard-observability.md).

## Advanced Dashboard

The AOS provides two main dashboards depending on your role:

* **Administrator Dashboard:** Displays cloud and observability data across all resources and infrastructures. Accessible only to Administrators.
* **Tenant Dashboard:** Displays cost and observability data scoped to the Tenant. Accessible to non-administrators with access to the selected Tenant.

### Accessing the Advanced Dashboard

Navigate to:

* **Administrator** → **Observability** → **Advanced** → **Dashboard** (Admin view)
* **Observability** → **Advanced** → **Dashboard** (Tenant view)

<figure><img src="../../../../.gitbook/assets/image (489).png" alt=""><figcaption></figcaption></figure>

## Logging

Click the **Logs** card on the AOS Dashboard.

The Grafana Logging dashboard opens, showing real-time logs for Services and Containers.

<figure><img src="../../../../.gitbook/assets/image (490).png" alt=""><figcaption></figcaption></figure>

Adjust filters to refine your view, or leave defaults to see all logs.

Optionally, click a log entry to view details, explore traces, or see context.

{% hint style="info" %}
Logs are powered by **Grafana Loki** and include metadata such as Tenant, Namespace, Pod, and Host for easier troubleshooting.
{% endhint %}

## Metrics

Click the **Metrics** card on the AOS Dashboard.

The Grafana Metrics dashboard opens, showing real-time performance metrics for your Services and Containers.

<figure><img src="../../../../.gitbook/assets/image (491).png" alt=""><figcaption></figcaption></figure>

Adjust filters or time intervals to focus on specific resources or trends, or leave defaults to see all metrics.

Optionally, click a metric or panel to explore details in Grafana for deeper analysis.

{% hint style="info" %}
Metrics are powered by **Grafana Mimir** and provide insights into CPU, memory, request rates, and errors for easier troubleshooting and monitoring.
{% endhint %}

## Other Observability Features

* **Cloud Spend:** View real-time cloud expenditures by Tenant, Service, or Infrastructure.
* **Kubernetes / Docker metrics:** Monitor CPU, memory, and container performance across workloads.
* **Traces (Tempo)**: Track request flows and latency.
* **Profiles (Pyroscope)**: Inspect application performance and CPU profiling.
* **Alerts (Alertmanager)**: Review and acknowledge active alerts.
* **Audit Logs:** Track user and system activity across your DuploCloud environment. See [Audit Logs](../5.-audit-logs.md) for details.&#x20;

Click any card to open the detailed Grafana dashboard for that feature.&#x20;

For full instructions and advanced usage, see the [AOS documentation](../../../../automation-platform/diagnostics-overview/advanced-observability-suite/).
