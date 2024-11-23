---
description: DuploCloud's Advanced Observability Suite Add-on
---

# Advanced Observability Suite

DuploCloud's Advanced Observability Suite (AOS) is an add-on service to boost your monitoring and troubleshooting abilities. Built on OpenTelemetry, our AOS leverages [Prometheus ](https://prometheus.io/)and [Grafana ](https://grafana.com/)to deliver robust, real-time observability for your cloud infrastructure. It includes real-time anomaly detection and customizable alerts and unifies metrics, traces, logs, and profiles to track all aspects of your environment easily.&#x20;

The Grafana-powered dashboards can be customized to spotlight key metrics and visualize trends in real time, empowering swift, data-driven decisions. DuploCloud’s AOS simplifies troubleshooting and enhances system health by providing a holistic view of your application and infrastructure performance.

### About OpenTelemetry

[OpenTelemetry ](https://opentelemetry.io/)is an open-source project from the Cloud Native Computing Foundation (CNCF) that supports multiple programming languages and environments. It provides a flexible, vendor-neutral framework for monitoring and analyzing application performance. Designed for high scalability, OpenTelemetry is ideal for distributed applications and helps reduce costs by using open-source components instead of expensive proprietary systems. See the [OpenTelemetry documentation](https://opentelemetry.io/docs/what-is-opentelemetry/) for more. &#x20;

## Advanced Observability Suite Use Cases

### Real-Time Monitoring and Observability

* **System Health Check**: Track real-time metrics like CPU usage, memory consumption, network traffic, and error rates across services to ensure that applications are healthy.
* **Latency Tracking**: Monitor request latencies to identify performance bottlenecks, particularly in services where latency spikes might indicate an issue.
* **Error Rate Analysis**: Track error counts and types to ensure services operate as expected and identify critical failure points.

### End-to-End Tracing and Dependency Mapping

* **Request Flow Visualization**: Visualize the path of requests through different services to understand interdependencies and identify which services may contribute to slowdowns or failures.
* **Service Dependency Mapping**: See which services interact with each other, allowing for a clear view of critical service dependencies and helping identify potential cascading failures.
* **Root Cause Analysis (RCA)**: Trace issues back to the source by identifying slow, failed, or error-prone transactions and drilling down to pinpoint problematic services or infrastructure.

### Performance Optimization

* **Identify Performance Bottlenecks**: Detect slow components, such as long-running queries, network delays, or overloaded services, and make data-driven decisions to optimize them.
* **Capacity Planning**: Use metrics to analyze usage patterns, forecast demand, and optimize resource allocation, helping avoid over-provisioning or under-resourcing.
* **Compare Release Impact**: Measure the impact of new releases on system performance by comparing metrics before and after deployments.

### Alerting and Incident Management

* **Set Alerts for Key Metrics**: Define thresholds and set alerts for anomalies in critical metrics, such as high error rates or slow response times, so that teams can act quickly.
* **Incident Response and Remediation**: Enable responders to access context-specific insights that accelerate incident response, diagnostics, and resolution times.
* **Service-Level Agreement (SLA) Monitoring**: Track SLA compliance metrics, such as uptime and latency, to ensure the system meets contractual obligations.

### User Experience Insights

* **Track User Journey Metrics**: Analyze performance metrics specific to different user journeys (e.g., checkout flows) to understand the impact of backend performance on user experience.
* **End-to-End Latency Perceptions**: Collect latency and success metrics for critical user actions to help understand where improvements could enhance user satisfaction.

### Security and Compliance Monitoring

* **Detect Anomalous Behavior**: Set up alerts on unusual patterns or outliers in metrics that could indicate potential security incidents.
* **Audit Logging**: Track API call/sensitive event logs (e.g., login attempts) to assist in compliance reporting and security auditing.

### Custom Business and Operational Metrics

* **Monitor Business KPIs**: Track custom metrics like transaction success rates, revenue per minute, or user engagement rates to tie technical performance to business outcomes.
* **Cost Optimization**: Identify underused resources or inefficient services to optimize operational costs and improve infrastructure utilization.

### Other Duplo-Specific Use Cases

* Request new capabilities via DuploCloud/Using the OpenTelemetry open-source API.

## Additional Functions

From the Grafana console, you can perform various tasks to customize your observability experience and proactively manage system health. For additional information, see the [Grafana documentation](https://grafana.com/docs/grafana/latest/).&#x20;
