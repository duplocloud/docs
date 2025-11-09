---
description: View billing data and create billing alerts for GCP billing data
---

# Viewing and Monitoring GCP Billing Data

From the DuploCloud portal, administrators can view account spending details by month, week, and Tenant. Non-administrator users can view billing data for a Tenant they have user access to.

In addition, DuploCloud allows you to set up billing alerts to monitor cloud spending and detect cost spikes early.&#x20;

## Prerequisites

* Complete the steps on the [Enable GCP billing data](export-billing-to-bigquery.md) page before attempting to view billing data in the portal.

## Viewing Account Billing Details

View the billing details for your company's GCP account.&#x20;

1. Log in as an administrator, and navigate to **Administrator** -> **Billing**. &#x20;

<figure><img src="../../../../.gitbook/assets/Screenshot (602).png" alt=""><figcaption><p>The account <strong>Billing</strong> page, <strong>Spend by Month</strong> tab for GCP</p></figcaption></figure>

You can view usage by:

* Time
  * Select the **Spend by Month** tab and click **More Details** to display monthly and weekly spending options. &#x20;
* Tenant
  * Select the **Spend by Tenant** tab.

## Viewing Tenant Billing Details

View billing details for a selected Tenant. This option is accessible to non-administrator users with user access to the selected Tenant.&#x20;

1. Select the **Tenant** name from the **Tenant** list box.&#x20;
2. Navigate to **Cloud Services** -> **Billing**. The **Billing** page displays.

<figure><img src="../../../../.gitbook/assets/Screenshot (603).png" alt=""><figcaption><p>The Tenant <strong>Billing</strong> page, <strong>Spend by Month</strong> tab</p></figcaption></figure>

The **Spend by Month** tab lists the five services with the highest spending for each month for the selected Tenant. Click **More Details** on any month's card to display more details about that month's spending. &#x20;

## Setting Up Billing Alerts

To monitor cloud costs based on usage, you can configure Billing Alerts in DuploCloud. For more details, see the [Billing Alerts documentation](../../../diagnostics-overview/configure-billing-alerts.md).

<figure><img src="../../../../.gitbook/assets/Screenshot (600) (4).png" alt=""><figcaption><p><strong>Billing</strong> page in the DuploCloud Portal with the <strong>Enable Billing Feature</strong> option highlighted</p></figcaption></figure>
