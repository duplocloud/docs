---
description: Configure infrastructure firewall rules in DuploCloud for GCP environments
---

# Infrastructure Firewall Rules

This page explains how to create and manage **infrastructure-level firewall rules** in DuploCloud for your Google Cloud Platform (GCP) environment. These firewall rules control inbound and outbound network traffic to your virtual machines and other infrastructure resources.

Rules define whether traffic is allowed or denied based on source IP ranges, protocols, ports, and targets. These rules are stateful, meaning return traffic is automatically allowed, and they apply broadly at the infrastructure level to secure your entire environment.

Common use cases for infrastructure firewall rules include:

* Allowing HTTP/HTTPS traffic to web servers
* Restricting SSH access to specific IP ranges
* Blocking traffic from known malicious IPs

You can create, update, and manage these firewall rules directly from the DuploCloud Portal.

## Creating an Infrastructure Firewall Rule

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**.
2. Click the infrastructure name in the **NAME** column.
3. Select the **Firewall Rules** tab.
4.  Click **Add**. The **Add Firewall Rule** pane displays.\


    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (586).png" alt="" width="299"><figcaption><p><strong>Add Firewall Rule</strong> pane </p></figcaption></figure></div>
5. Complete the fields:

<table data-header-hidden><thead><tr><th width="217.5555419921875">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for the rule.</td></tr><tr><td><strong>Description</strong></td><td>Optionally, enter a description explaining the rule’s purpose.</td></tr><tr><td><strong>Source Type</strong></td><td>Select the source type for the firewall rule (e.g., <strong>IPv4 ranges</strong>).</td></tr><tr><td><strong>Source Value</strong></td><td>Enter the IP address or CIDR range(s) that define the source of the traffic, e.g., <code>10.0.0.0</code> or <code>10.0.0.0/8</code>.</td></tr><tr><td><strong>Action</strong></td><td>Choose <strong>Allow</strong> or <strong>Deny</strong>.</td></tr><tr><td><strong>Protocol and Ports</strong></td><td>Choose <strong>Allow all</strong> to permit all protocols and ports, or <strong>Specified protocols and ports</strong> to define particular protocols (<strong>TCP</strong>, <strong>UDP</strong>, <strong>SCTP</strong>, etc.) and port ranges.</td></tr></tbody></table>

6. Click **Add** to create the firewall rule.&#x20;

{% hint style="info" %}
**Tip:** Use clear, descriptive names, follow the principle of least privilege by only allowing required traffic, and regularly audit rules to remove unused or overly permissive entries.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/Screenshot (589).png" alt=""><figcaption><p><strong>Firewall Rules</strong> tab for the Auto infrastructure</p></figcaption></figure>

## Managing Existing Infrastructure Firewall Rules

Edit or delete firewall rules directly from the DuploCloud Portal.&#x20;

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**.
2. Click the infrastructure name in the **NAME** column.
3. Select the **Firewall Rules** tab.
4. Click the menu icon (<img src="../../../../.gitbook/assets/menu icon (2) (2).avif" alt="" data-size="line">) in the row of the firewall rule you want to manage.
5.  Choose one of the following options:

    * **Edit**: Opens the **Update Firewall Rule** pane to modify the firewall rule configuration.
    * **Remove Rule**: Deletes the firewall rule after confirmation.\


    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (587).png" alt=""><figcaption><p>Firewall rule menu options highlighted in the DuploCloud Portal</p></figcaption></figure></div>

