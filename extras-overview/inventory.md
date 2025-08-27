---
description: View all cloud resources in your environment on the DuploCloud Inventory page
---

# Inventory

The Inventory page in DuploCloud provides a centralized view of all cloud resources across your environment, providing a quick way to see everything you have deployed in one place.

You can use the Inventory page to:

* Locate resources without navigating through multiple tenants or service pages.
* Verify that deployments have completed.
* Cross-check counts across services.
* Audit your environment for troubleshooting or compliance purposes.
* Export a full inventory of cloud resources for recordkeeping or compliance needs.

{% hint style="info" %}
For Host-level security inventory collected via OSSEC and visible in the SIEM dashboard, see the [**Inventory Monitoring** documentation](../security-and-compliance/access-control-3/inventory.md) in the **Security and Compliance** section.
{% endhint %}

## Accessing the Inventory Page

The Inventory page displays a full list of resources for recordkeeping, troubleshooting, or compliance purposes.

1. Navigate to **Administrator** → **Inventory**. The **Inventory** page displays.&#x20;

<figure><img src="../.gitbook/assets/Screenshot (788).png" alt=""><figcaption><p><strong>Inventory</strong> page</p></figcaption></figure>

2.  Select a tab at the top to filter resources by category. The tabs vary depending on the cloud provider and your environment.\


    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (789).png" alt=""><figcaption><p><strong>Host</strong> tab on the <strong>Inventory</strong> page</p></figcaption></figure></div>
3.  Click any resource name in the list to drill down to more detailed information about that resource.\


    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (790).png" alt=""><figcaption><p><strong>EC2</strong> tab on the <strong>Inventory</strong> page</p></figcaption></figure></div>

## Downloading an Inventory Report

DuploCloud allows users to export a full list of resources from the **Inventory** page:&#x20;

1. Navigate to **Administrator** -> **Inventory**. The **Inventory** page displays.&#x20;
2. Select the **All Resources** tab.
3.  Click the button in the upper right to export your inventory. The exact button and file format vary by cloud provider:

    * **AWS:** Click **DuploCloud Inventory Report** to download a compliance-ready Excel (`.xlsx`) report containing all AWS resource details. Useful for audits and StateRAMP/FedRAMP compliance.
    * **GCP and Azure**: Click **Export to CSV** to download an operational snapshot in CSV format of DuploCloud-managed resources. Primarily used for troubleshooting or recordkeeping.\


    <figure><img src="../.gitbook/assets/Screenshot (792).png" alt=""><figcaption><p><strong>Inventory</strong> page with <strong>DuploCloud Inventory Report</strong> option highlighted</p></figcaption></figure>
