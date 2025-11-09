---
description: Configure custom metrics  for DuploCloud’s Advanced Observability Suite (AOS)
---

# Custom Metrics

DuploCloud’s Advanced Observability Suite (AOS) supports custom metrics collection and visualization, enabling you to monitor application-specific metrics in addition to default Kubernetes metrics. This guide will walk you through the steps to configure your applications to expose custom metrics and make them available in DuploCloud AOS.

## Configuring Annotations for Scraping Custom Metrics

```
k8s_grafana_com_scrape: true
k8s_grafana_com_job: custom-metrics
k8s_grafana_com_metrics_path: /metrics
k8s_grafana_com_metrics_portNumber: 9100
```
