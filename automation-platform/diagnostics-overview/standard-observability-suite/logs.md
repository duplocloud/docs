---
description: >-
  Logging in the DuploCloud Standard Observability Suite utilizing OpenSearch
  and Kibana
---

# Logs

DuploCloud Standard Observability Suite uses built-in OpenSearch for log storage and search. Filebeat is the collector deployed on each host to gather logs from containers and other system services.&#x20;

Logs can be accessed at the platform level (by Administrators), at the Tenant level, or directly from a specific Service using the Logs link.

## Viewing Platform Logs

Use this option to view logs across all tenants or to troubleshoot issues at the platform level.

1. Navigate to **Administrator** → **Observability** → **Standard** → **Logging** in the DuploCloud Portal.

This page includes two tabs:

* **Main**: Shows logs using an embedded OpenSearch dashboard provided by DuploCloud. You can select a Tenant and use filters to find the logs you need.
* **Kibana**: Available if your organization has set up a custom Kibana (OpenSearch) URL. This lets you view logs with more advanced tools and features.

<figure><img src="../../../.gitbook/assets/Screenshot (721).png" alt=""><figcaption></figcaption></figure>

## Viewing Tenant Logs

Use this view to access logs scoped to a single tenant.

1. Navigate to **Observability** → **Standard** → **Logging**.

In this view:

* Logs are automatically filtered to show only data for the current tenant.
* At the top, use the **Service** dropdown to filter logs for a specific service.
* Alternatively, click **Search by Filters** to create custom filters for more precise log searching.

<figure><img src="../../../.gitbook/assets/Screenshot (724).png" alt=""><figcaption></figcaption></figure>

## Viewing Service-Specific Logs

You can quickly access logs filtered for a Specific service directly from the Service details page. This shortcut helps you troubleshoot service issues faster without manually applying filters.

To view logs for a Service:

1. Navigate to **Kubernetes** → **Services** (or the relevant service list) in the DuploCloud Portal.
2. Click the menu icon (<img src="../../../.gitbook/assets/menu icon (20).avif" alt="" data-size="line">) next to the Service you want to view logs for.
3. Select **Logs**. This will open a logs dashboard pre-filtered to show logs for that specific service.

## Application log retention policy

DuploCloud retains application logs in two stages: comprehensive tracking and auditing.&#x20;

Initially, logs are available in OpenSearch for 60 days, ensuring immediate access for recent activity analysis.&#x20;

Logs are archived in an S3 Bucket for 365 days for long-term storage, meeting compliance, and historical data review needs. You can customize retention periods to meet specific requirements, offering flexibility in log management.
