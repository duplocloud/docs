---
description: Set up billing alerts to track cloud spending in DuploCloud
---

# Configuring Billing Alerts

Set billing alerts based on the previous month's spending or define a custom threshold. Receive email notifications if the current month's expenses exceed a specified percentage of the threshold.

{% hint style="info" %}
New billing alerts may take up to 24 hours to send their first message.
{% endhint %}

Set up billing alerts in DuploCloud to monitor and manage AWS cloud spending. Alerts can help you stay within budget by notifying you when expenses exceed a defined threshold. DuploCloud supports two types of billing alerts:

* **Administrator Billing Alerts** monitor total usage across all Tenants.
* **Tenant Billing Alerts** track spending within an individual Tenant.

Each alert compares current monthly usage against either the previous month’s spending or a custom threshold, and sends email notifications when a specified percentage is reached.

## Creating a Billing Alert

Billing alerts can be created at two levels: **Administrator** alerts monitor overall cloud spending across all tenants, while **Tenant** alerts focus on the usage within a specific Tenant. Choose the appropriate section in the DuploCloud Portal based on the scope you want to monitor.

1. In the DuploCloud Portal, navigate to **Administrator** → **Billing** for Administrator-level alerts or **Cloud Services** → **Billing** for Tenant-level alerts.
2.  Click **Add** to create a new billing alert. The **Add Billing Alert Config** pane displays.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (552).png" alt=""><figcaption><p><strong>Add Billing Alert Config</strong> pane</p></figcaption></figure></div>
3. Complete the fields (shown in the table below) according to your alert preferences.

<table data-header-hidden><thead><tr><th width="274.4444580078125"></th><th></th></tr></thead><tbody><tr><td><strong>Alert Name</strong></td><td>Enter a unique name for the billing alert.</td></tr><tr><td><strong>Choose Threshold</strong></td><td>Select the threshold type:<br>• <strong>Custom Threshold</strong>: Set your own spending threshold. <br>• <strong>Previous Month Spend</strong>: use the total spend from the prior month as the threshold.</td></tr><tr><td><strong>Threshold (Dollar Amount)</strong></td><td>Enter the dollar amount that triggers the alert (for Custom Thresholds only).</td></tr><tr><td><strong>Alert Trigger % (Percent of Threshold)</strong></td><td>Select the percentage of your defined threshold at which the alert should trigger. For example, 80% means you'll be notified when spending reaches 80% of the threshold.</td></tr><tr><td><strong>Azure Subscription</strong> <em>(Azure only)</em></td><td>Required for Azure billing alerts. Select the Azure Subscription to monitor.</td></tr><tr><td><strong>Google Project ID</strong> <em>(GCP only)</em></td><td>Required for GCP billing alerts. Select the GCP project to monitor.</td></tr><tr><td><strong>Tenant: Cost Tag (Optional)</strong><br><em>(Admin billing alerts only)</em></td><td>For Administrator-level billing alerts, select one or more Tenants to apply the alert to (e.g., <strong>All</strong>, <strong>Shared</strong>, or specific Tenants).</td></tr><tr><td><strong>Service (Optional)</strong></td><td>Optionally, select one or more DuploCloud Services to monitor as part of this alert.</td></tr><tr><td><strong>Email Notifications</strong></td><td>Select the email address that should receive the alert notifications.</td></tr><tr><td><strong>Pause Alerts</strong></td><td>Enable this setting to temporarily pause the alert.</td></tr></tbody></table>

4.  Click **Submit** to save your alert. The alert appears in the **Billing Alerts** tab and will trigger email notifications when conditions are met.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (556).png" alt=""><figcaption><p><strong>Billing Alerts</strong> tab displaying the <code>monthly_alert</code> billing alert</p></figcaption></figure></div>

## Viewing Billing Alerts

To view detailed information about a billing alert:

1. In the DuploCloud Portal, navigate to **Administrator** → **Billing** for Administrator-level alerts or **Cloud Services** → **Billing** for Tenant-level alerts.
2. Select the **Billing Alerts** tab.
3. Select the billing alert you want to view from the **NAME** column.
4. Use the tabs to explore alert details:

<table data-header-hidden><thead><tr><th width="300.22216796875"></th><th></th></tr></thead><tbody><tr><td><strong>Configuration</strong></td><td>Overview of the billing alert settings.</td></tr><tr><td><strong>Notification Filter by Service</strong></td><td>Services selected for this alert.</td></tr><tr><td><strong>Notification Email List</strong></td><td>Email addresses receiving alerts.</td></tr><tr><td><strong>Details</strong></td><td>Raw JSON configuration of the alert.</td></tr></tbody></table>

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot (557).png" alt=""><figcaption><p><strong>Configuration</strong> tab on the <code>monthly_alert</code> details page</p></figcaption></figure></div>

## Managing Billing Alerts

You can view billing alert details, edit alert configurations, or delete alerts as needed directly from the DuploCloud Platform.

1. In the DuploCloud Portal, navigate to **Administrator** → **Billing** for Administrator-level alerts or **Cloud Services** → **Billing** for Tenant-level alerts.
2. Select the **Billing Alerts** tab.
3. Click the menu icon (<img src="../../.gitbook/assets/menu icon (15).avif" alt="" data-size="line">) in the row of the billing alert you want to manage.
4. Select one of the following options:

<table data-header-hidden><thead><tr><th width="172.22216796875"></th><th></th></tr></thead><tbody><tr><td><strong>Details</strong></td><td>View the billing alert configuration in JSON format.</td></tr><tr><td><strong>Edit</strong></td><td>Open the <strong>Update Billing Alert Config</strong> pane to modify alert settings.</td></tr><tr><td><strong>Delete</strong></td><td>Permanently delete the billing alert (confirmation required).</td></tr></tbody></table>

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot (553).png" alt=""><figcaption><p><strong>Billing Alerts</strong> tab with menu options</p></figcaption></figure></div>

## Additional Resources

For cost management and billing data details related to your specific cloud provider, see the associated sections in the DuploCloud documentation:

* [AWS Billing and Cost Management](../overview/use-cases/cost-management/)
* [GCP Billing and Cost Management](../overview-1/use-cases/cost-management/)
* [Azure Billing and Cost Management](../overview-2/use-cases/billing-and-cost-management/)
