---
description: Viewing faults and alerts in the DuploCloud Portal
---

# Faults and Alerts

Faults that happen in the system, be it Infrastructure creation, container deployments, Application health checks, or any Triggered Alarms can be tracked in the DuploCloud portal under Faults Menu.

## Viewing Faults <a href="#id-1-toc-title" id="id-1-toc-title"></a>

You can look at Tenant-specific faults under **Observability** -> **Faults** or all the faults in the system under **Administrator** -> **Faults**.

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.20-14_04_51 (1).png" alt=""><figcaption><p>The <strong>Faults</strong> page showing faults for the DEV01 Tenant</p></figcaption></figure>

## Configuring Tenant Fault Settings <a href="#id-2-toc-title" id="id-2-toc-title"></a>

To configure faults for a Tenant, navigate to **Administrator** -> **Tenants** and select the Tenant from the **NAME** column. In the **Settings** tab, click **Add**. Select or enter the appropriate feature on the **Add Tenant Feature** pane.

DuploCloud provides tenant-level settings that control fault behavior across different workloads and services. Some settings specifically affect Kubernetes pods and jobs, while others apply to the Tenant more generally.

For instructions on adding or updating these settings, see the **Tenant Settings page** for your cloud provider:

* [AWS Tenant Settings](../../overview/aws-systems-settings/aws-tenant-settings.md)
* [Azure Tenant Settings](../../overview-2/azure-systems-settings/azure-tenant-settings.md)
* [GCP Tenant Settings](../../overview-1/gcp-systems-settings/gcp-tenant-settings.md)

### Tenant Fault Settings

<table><thead><tr><th width="401.91363525390625">Tenant Setting</th><th>Description</th></tr></thead><tbody><tr><td><code>raise_fault_on_last_state_pod_failure_reasons</code></td><td>Generates a fault when a Kubernetes pod is terminated with a specified failure reason. Enter the failure reasons you want to monitor, e.g., <code>OOMKilled</code>. Multiple reasons can be semicolon-separated.</td></tr><tr><td><code>enable_k8s_job_fault_logging</code></td><td>Generates faults for Kubernetes Job failures by default when set to <code>True</code>.</td></tr><tr><td><code>tenant_instances_stopped</code></td><td>Mutes faults for Tenants that have been stopped when set to <code>True</code>.</td></tr></tbody></table>

## Creating Alerts <a href="#id-2-toc-title" id="id-2-toc-title"></a>

Alerts in DuploCloud are created for individual resources and their metrics. To create an alert:

1. Navigate to the resource type you want to monitor:
   * For Kubernetes services: **Kubernetes** → **Services**
   * For RDS databases: **Cloud Services** → **Databases** → **RDS**
   * For other resources, follow a similar pattern
2. Select the resource from the **NAME** column to open its details page.
3. Click the **Alerts** tab.
4.  Click **Add**. The **Create Alert** pane displays.\


    <div align="left"><img src="../../.gitbook/assets/Screenshot (891).png" alt="Create Alert pane" width="409"></div>
5. Enter the desired threshold, conditions, and notification options.
6. Click **Create** to save the alert.

## Viewing Alerts

### General Alerts

General alerts show all alerts across your account and all resources, providing a high-level view of system-wide issues.

1. Navigate to **Observability** -> **Alerts**.

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.20-16_03_17 (1).png" alt=""><figcaption><p>General <strong>Alerts</strong> page under <strong>Observability</strong> in the DuploCloud Portal</p></figcaption></figure>

### Resource-Specific Alerts

Resource-specific alerts display only the alerts associated with a particular resource, such as a Service, Host, or Database, allowing you to focus on issues affecting that specific component.

1. Navigate to the resource’s details page (see the steps in [Creating Alerts](./#id-2-toc-title-1) above).
2. Select the **Alerts** tab.

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.20-16_05_28 (1).png" alt=""><figcaption><p><strong>Alerts</strong> tab under <strong>Cloud Services</strong> -> <strong>Hosts</strong> in the DuploCloud Portal</p></figcaption></figure>
