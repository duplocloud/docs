---
description: >-
  Using profiles with Pyroscope in the DuploCloud Advanced Observability Suite
  (AOS)
---

# Profiles with Pyroscope

A profile is essentially a snapshot of your application's performance metrics at a specific point in time. DuploCloud’s Advanced Observability Suite (AOS) uses [Pyroscope](https://pyroscope.io/) to provide detailed application profiles. These profiles give you detailed insights into how resources like CPU and memory are being used and help you optimize performance and monitor resource usage.&#x20;

Pyroscope integrates seamlessly with DuploCloud’s other observability tools, like Tempo (for tracing) and Beyla (for telemetry). This allows you to view profiling data alongside traces and logs in Grafana for a unified monitoring experience. The combination of automatic profiling with the option for manual fine-tuning using OpenTelemetry SDKs helps capture the most relevant data for optimizing application performance.

By default, CPU profiles are collected for all applications, while memory profiles are specifically collected for Go and Java applications, providing deeper insights into performance and resource utilization.

## **Enabling Profiling**

To enable application profiling, you can push profiling data directly to Pyroscope by [instrumenting your application](application-instrumentation.md). For detailed instructions on configuring the client, refer to the [Pyroscope documentation](https://grafana.com/docs/pyroscope/latest/configure-client/).

## **What Profiles Can Tell You**

Pyroscope is the backend for profiles that show the CPU and Memory profile for the application. Exploring profiles helps identify and resolve performance issues, optimize resource usage, and improve efficiency. Key benefits include:

* **Identifying Performance Bottlenecks**: Pinpointing slow functions or resource-heavy processes.
* **Optimizing Resource Utilization**: Analyzing CPU and memory usage for better scaling decisions.
* **Debugging Latency Issues**: Detecting areas with high latency that may affect user experience.
* **Root Cause Analysis**: Correlating profiling data with logs and traces to identify the cause of performance issues.

For more information about profile data, see the [Grafana Pyroscope documentation](https://grafana.com/docs/pyroscope/latest/view-and-analyze-profile-data/flamegraphs/).&#x20;

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption><p>The Grafana <strong>Profiling</strong> Dashboard</p></figcaption></figure>
