---
description: Instrument applications in DuploCloud using Grafana Beyla and OpenTelemetry
---

# Application Instrumentation

DuploCloud leverages automated instrumentation with [Grafana Beyla](https://grafana.com/docs/beyla/latest/) and the [OpenTelemetry Operator](https://opentelemetry.io/docs/kubernetes/operator/) to provide robust monitoring and tracing without extensive manual configuration. With Grafana Beyla, users get automatic instrumentation out of the box for a wide range of languages, capturing key metrics and trace spans with minimal setup. For languages and use cases not covered by Beyla, users can manually instrument their applications using OpenTelemetry, offering full flexibility to capture detailed telemetry data where automated options are unavailable.

## Automated instrumentation using Beyla

* **Grafana Beyla** is an open-source, eBPF-based auto-instrumentation tool designed to simplify the collection of key observability data for applications written in Go, C/C++, Rust, Python, Ruby, Java, NodeJS, .NET, and more.
* It uses eBPF technology to capture RED metrics (Rate, Error, Duration) and basic trace spans for HTTP/S and gRPC services running on Linux, without requiring code changes or configuration updates.
* Beyla is ideal for getting started quickly with observability and provides a low-overhead way to monitor application performance.

For more information, see the [Beyla documentation](https://grafana.com/oss/beyla-ebpf/).&#x20;

## **OpenTelemetry Operator for Advanced Tracing**

While Beyla captures foundational metrics and spans out of the box, it does not provide distributed tracing or detailed trace spans. To address this, DuploCloud integrates the Kubernetes OpenTelemetry Operator.

* This operator enables auto-instrumentation for services written in .NET, Java, Node.js, Python, and Go based on **Pod Annotations**.
* DuploCloud ships an **Instrumentation object** in the OTEL namespace by default, forwarding telemetry data to an OpenTelemetry Collector (Alloy).
* The following annotations are used for different programming languages to enable automatic instrumentation:
  * .NET: `instrumentation.opentelemetry.io/inject-dotnet: "`duploservices-<\<Opentelemetry\_tenant>>/otel-instrumentation`"`
  * Go: `instrumentation.opentelemetry.io/inject-go: "`duploservices-<\<Opentelemetry\_tenant>>/otel-instrumentation`"`
  * Java: `instrumentation.opentelemetry.io/inject-java: "`duploservices-<\<Opentelemetry\_tenant>>/otel-instrumentation`"`
  * Node.js: `instrumentation.opentelemetry.io/inject-nodejs: "`duploservices-<\<Opentelemetry\_tenant>>/otel-instrumentation`"`
  * Python: `instrumentation.opentelemetry.io/inject-python: "`duploservices-<\<Opentelemetry\_tenant>>/otel-instrumentation`"`
* Users can also customize or add OpenTelemetry environmental variables for their Pods, as needed. See the [OpenTelemetry documentation](https://opentelemetry.io/docs/kubernetes/operator/automatic/) for details.&#x20;

## Manual instrumentation

For applications using unsupported languages or scenarios not covered by automated tools, manual instrumentation is recommended. OpenTelemetry offers libraries and documentation to help developers manually instrument applications across a variety of languages and frameworks. Refer to the [OpenTelemetry documentation](https://opentelemetry.io/docs/concepts/instrumentation/) for detailed guidance on how to integrate OpenTelemetry into your application.

When instrumenting your application, you need to configure telemetry endpoints dynamically to send telemetry data (such as traces, metrics, and logs) to the OpenTelemetry Collector. This configuration is done by setting the appropriate environment variables (EVs) in your application.

<table data-header-hidden><thead><tr><th width="397"></th><th></th></tr></thead><tbody><tr><td><strong>Environment Variable (EV)</strong></td><td><strong>Endpoint URL</strong></td></tr><tr><td><code>OTEL_EXPORTER_OTLP_TRACES_ENDPOINT</code></td><td><code>http://duplo-tracing.duploservices-Opentelemetry_tenant/v1/traces</code></td></tr><tr><td><code>OTEL_EXPORTER_OTLP_METRICS_ENDPOINT</code></td><td><code>http://duplo-metrics-distributor.duploservices-Opentelemetry_tenant/api/v1/push</code></td></tr><tr><td><code>OTEL_EXPORTER_OTLP_LOGS_ENDPOINT</code></td><td><code>http://duplo-logging.duploservices-Opentelemetry_tenant:3100/loki/api/v1/push</code></td></tr></tbody></table>

### **Manual instrumentation for Kubernetes (within the Cluster)**

To manually instrument your application in a Kubernetes environment, set the OTEL (OpenTelemetry) environment variables in your Kubernetes deployment configuration. These environment variables will direct telemetry data (traces, metrics, and logs) to the OpenTelemetry Collector.

1. Set the required environment variables for OpenTelemetry in your application’s Kubernetes deployment YAML.
2. Use the appropriate endpoint URLs for OpenTelemetry.

### **Manual instrumentation for external applications (outside Kubernetes)**

If your application is running outside of a Kubernetes cluster, contact DuploCloud Support for assistance. DuploCloud will expose endpoints via Kubernetes Ingress and provide the necessary URLs for your external application.

1. Once the URLs are provided by DuploCloud, configure your application to use them.
2. Set the environment variables in your external application, replacing the endpoint URLs with those provided by DuploCloud.

## Custom Metrics

If your application exposes custom metrics in a Prometheus-compatible format, you can easily integrate these metrics into your monitoring stack. By following the steps below, your custom metrics will be automatically scraped and stored in the database for visualization and analysis.

1. Expose Metrics on a Container Port and Path: Ensure your application exposes the custom metrics on a specific port and path within the container. For example, metrics might be available at `http://<pod-ip>:9100/metrics`.
2. Add Kubernetes Annotations: To enable automatic scraping of these metrics, add the following annotations to your Kubernetes pod specification:

```
  k8s_grafana_com_scrape: "true"
  k8s_grafana_com_job: "custom-metrics"
  k8s_grafana_com_metrics_path: "/metrics"
  k8s_grafana_com_metrics_portNumber: "9100"
```

Once these annotations are set, your application’s custom metrics will be collected and can be visualized in Grafana.

Alternatively, DuploCloud can expose the OTEL (OpenTelemetry) endpoint, and you can push your custom metrics using the OTLP protocol.
