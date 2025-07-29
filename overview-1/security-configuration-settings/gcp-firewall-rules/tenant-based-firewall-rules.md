---
description: Configure Tenant-based firewall rules in DuploCloud for GCP environments
---

# Tenant-Based Firewall Rules

This page explains how to create and manage Tenant-based firewall rules in DuploCloud for your Google Cloud Platform (GCP) environment. Tenant firewall rules control network traffic at the Tenant level within your infrastructure, enabling you to set access policies specific to individual Tenants.

These rules provide isolation and customized security boundaries between Tenant workloads, helping you enforce Tenant-specific network controls.

Common use cases for Tenant firewall rules include:

* Permitting communication between trusted Tenants
* Restricting access to sensitive services within a Tenant
* Blocking malicious traffic targeting a Tenant’s resources

You can create, update, and manage Tenant firewall rules directly from the DuploCloud Portal, giving you granular control over multi-Tenant environments.

## Adding a Tenant-Based Firewall Rule

1. In the DuploCloud Portal, navigate to **Administrator** -> **Tenants**.
2. From the **NAME** column, click the Tenant name where you want to add the firewall rule.
3. Select the **Firewall Rules** tab.
4.  Click the **Add** button. The **Add Firewall Rule** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (638).png" alt=""><figcaption><p><strong>Add Firewall Rule</strong> pane</p></figcaption></figure></div>
5. Configure the fields, as described below:

<table data-header-hidden><thead><tr><th width="217.5555419921875">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Rule Type</strong></td><td>Choose <strong>Tenant</strong> to apply the rule based on Tenant traffic, or <strong>IP Address</strong> to apply it based on specific IP ranges.</td></tr><tr><td><strong>Source Tenant</strong><br><em>(for Tenant rule type)</em></td><td>Select the Tenant from which the traffic originates.</td></tr><tr><td><strong>Name</strong></td><td>Enter a unique name for the firewall rule.</td></tr><tr><td><strong>Description</strong></td><td>Optionally, provide a description explaining the purpose of this rule.</td></tr><tr><td><strong>Source Type</strong></td><td>Specify the type of source address (e.g., <strong>IPv4 ranges</strong>).</td></tr><tr><td><strong>Source Value</strong></td><td>Enter the IP address or range in CIDR notation (e.g., <code>10.0.0.0</code>, <code>10.0.0.0/8</code>).</td></tr><tr><td><strong>Action</strong></td><td>Choose to <strong>Allow</strong> or <strong>Deny</strong> the traffic matching this rule.</td></tr><tr><td><strong>Protocol and Ports</strong></td><td>Select <strong>Allow All</strong> to allow all protocols and ports, or <strong>Specified protocols and ports</strong> to restrict traffic. <br><br>If you selected <strong>Specified protocols and ports</strong>, enter ports or port ranges for each protocol as needed: <strong>TCP</strong>, <strong>UDP</strong>, <strong>SCTP</strong> (e.g., <code>20,25-100</code>), and <strong>Other</strong> protocols.</td></tr></tbody></table>

6. Click **Add** to create the firewall rule.

<figure><img src="../../../.gitbook/assets/Screenshot (639).png" alt=""><figcaption><p><strong>Firewall Rules</strong> tab in the DuploCloud Portal</p></figcaption></figure>

## Managing Existing Tenant-Based Firewall Rules

Edit or delete firewall rules directly from the DuploCloud Portal.&#x20;

1. In the DuploCloud Portal, navigate to **Administrator** -> **Tenants**.
2. Click the Tenant  name in the **NAME** column.
3. Select the **Firewall Rules** tab.
4. Click the menu icon (<img src="../../../.gitbook/assets/menu icon (2) (2).avif" alt="" data-size="line">) in the row of the firewall rule you want to manage.
5.  Choose one of the following options:

    * **Edit**: Opens the **Update Firewall Rule** pane to modify the firewall rule configuration.
    * **Remove Rule**: Deletes the firewall rule after confirmation.\


    <figure><img src="../../../.gitbook/assets/Screenshot (613).png" alt=""><figcaption><p><strong>Firewall Rules</strong> tab in the DuploCloud Portal</p></figcaption></figure>
