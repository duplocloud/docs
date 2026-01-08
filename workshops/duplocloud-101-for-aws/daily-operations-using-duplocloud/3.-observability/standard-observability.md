---
description: >-
  Viewing Standard logs, metrics, and resource health for your Services and
  Hosts.
---

# Standard Observability

**Standard Observability** provides basic monitoring for Services and Containers, including logs, metrics, and cloud spend.&#x20;

DuploCloud also offers an add-on observability service called the Advanced Observability Suite (AOS). For daily operations using the AOS, see [Advanced Observability Suite (AOS)](advanced-observability-suite-aos.md).&#x20;

## Prerequisites

* **Set up the Standard Observability Suite** for your Infrastructure. For instructions on enabling logging and metrics, see [Setup for the Standard Observability Suite](https://docs.duplocloud.com/docs/automation-platform/diagnostics-overview/standard-observability-suite/setup).

## Standard Dashboard

### Accessing the Standard Dashboard

1. Navigate to the Standard Observability dashboard:
   * For Administrators, navigate to: **Administrator** → **Observability** → **Standard** → **Dashboard**
   * For Tenant users, navigate to: **Observability** → **Standard** → **Dashboard**

The Dashboard shows a high-level overview of your Tenant’s cloud resources and usage including:

* **Cloud Spend:** Current month and top services by cost.
* **Resources:** Counts of Services, Containers, Databases, Buckets, and any Faults.
* **Kubernetes / Docker:** Deployed Services and Containers.
* **Logs:** Access and view logs collected from Services and Containers.
* **Metrics:** Monitor CPU, memory, and other performance metrics for your resources.

<figure><img src="../../../../.gitbook/assets/Screenshot (1063).png" alt=""><figcaption></figcaption></figure>

## Logging

### Viewing Logging with OpenSearch

1. From the Standard Dashboard, click **Logs** to view log data in OpenSearch.
2. Choose what to view:
   * **Administrators:** Filter logs by Tenant using the **Tenant** list box.
   * **Tenant users:** Filter logs by Service using the **Service** list box.

<figure><img src="../../../../.gitbook/assets/image (492).png" alt=""><figcaption><p>Logging data for the nginx Service</p></figcaption></figure>

## Metrics

### Viewing Metrics

1.  To access metrics in Standard Observability, choose the appropriate navigation path based on the scope you need:

    * **Resource-wide metrics for administrators:** navigate to **Administrator** → **Observability** → **Standard**, and click **Metrics**.
    * **Tenant-level metrics**: navigate to **Observability** → **Standard**, and click **Metrics**.



<figure><img src="../../../../.gitbook/assets/image (495).png" alt=""><figcaption></figcaption></figure>

## Other Observability Features

* **Cloud Spend:** View current month spending and top services by cost.
* **Kubernetes / Docker metrics:** Monitor CPU, memory, and container performance for your Services and Containers.
* **Audit Logs:** Track user and system activity across your DuploCloud environment. See [Audit Logs](../5.-audit-logs.md) for details.&#x20;

Click any card to open the corresponding dashboard for more details.\
\
For advanced observability features, see the [Standard Observability documentation](../../../../automation-platform/diagnostics-overview/standard-observability-suite/).
