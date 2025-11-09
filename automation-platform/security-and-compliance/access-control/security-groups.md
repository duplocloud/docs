---
description: DuploCloud Tenants and Security Groups
---

# Security Groups

<div align="left"><figure><img src="../../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption><p><strong>Add Tenant Security</strong> pane</p></figcaption></figure></div>

In DuploCloud, each Tenant is associated with its own Security Group, which allows unrestricted communication between all resources within that Tenant. This setup ensures that any computing resource in that Tenant can easily reach the services within that same Tenant.

## Managing Security Groups in DuploCloud

### Allowing Inter-Tenant Access

Administrators can allow inter-Tenant traffic using the **Add Tenant Security** pane:

1. From the DuploCloud Portal, navigate to **Administrator** -> **Tenants**.
2. Select the Tenant you want to open from the **NAME** column.
3. Select the **Security** tab.&#x20;
4.  Click **Add**. The **Add Tenant Security** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (325).png" alt="" width="359"><figcaption><p>The <strong>Add Tenant Security</strong> pane </p></figcaption></figure></div>
5. Complete the fields:

<table data-header-hidden><thead><tr><th width="140.22222900390625"></th><th></th></tr></thead><tbody><tr><td><strong>Source Type</strong></td><td>Select the source of incoming traffic:<br>- <code>Tenant</code> – Allow access from another DuploCloud Tenant<br>- <code>IP Address</code> – Allow access from a specific IP or VPN range</td></tr><tr><td><strong>Tenant</strong></td><td><em>(If Source Type = Tenant)</em> Select the Tenant you want to allow access from.</td></tr><tr><td><strong>IP CIDR</strong></td><td><em>(If Source Type = IP Address)</em> Choose:<br>- <code>Custom</code> to manually enter an IP or CIDR<br>- <code>VpnIp</code> to allow access from VPN-connected clients (no IP input needed)</td></tr><tr><td></td><td><em>(If IP CIDR Type = Custom)</em> Enter a specific IP or CIDR (e.g., <code>203.0.113.10</code> or <code>10.1.0.0/16</code>).</td></tr><tr><td><strong>Protocol</strong></td><td>Choose from: <code>TCP</code>, <code>UDP</code>, or <code>ICMP</code>.</td></tr><tr><td><strong>Port Range</strong></td><td>(<em>If Protocol =TCP or UDP)</em> Specify the port range. </td></tr><tr><td><strong>Description</strong></td><td>Optionally, enter a brief note about the rule’s purpose.</td></tr></tbody></table>

6. Click **Add**. Inter-Tenant access is configured.&#x20;

### **Configuring Azure VNet Security**

In Azure, security is implemented at the **Virtual Network (VNet)** level. All traffic within the VNet is allowed by default. However, Administrators can override this behavior by setting up security rules to control traffic between different VNets or from a VNet to external resources.

1. From the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**.
2. Select the Infrastructure you want to manage access for from the **NAME** column.
3. Select the **Security Group Rules** tab.&#x20;
4.  Click **Add**. The **Add Infrastructure Security** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (327).png" alt=""><figcaption><p>The <strong>Add Infrastructure Security</strong> pane</p></figcaption></figure></div>
5. Complete the fields:

<table data-header-hidden><thead><tr><th width="175.77777099609375"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>A unique name for the rule.</td></tr><tr><td><strong>Subnet</strong></td><td>The subnet this rule will apply to (e.g., <code>custom-default</code>).</td></tr><tr><td><strong>Direction</strong></td><td>Whether the rule applies to <code>Inbound</code> or <code>Outbound</code> traffic.</td></tr><tr><td><strong>Source Type</strong></td><td>The source of the traffic: <code>IP Address</code>, <code>Service Tag</code>, or <code>Application Security Group</code>.</td></tr><tr><td><strong>Source Value</strong></td><td>IP/CIDR (e.g., <code>10.0.0.0/8</code>), service tag (e.g., <code>Internet</code>), or ASG name.</td></tr><tr><td><strong>Source Port Range</strong></td><td>Port or port range from the source (e.g., <code>*</code>, <code>443</code>, <code>1000-2000</code>).</td></tr><tr><td><strong>Destination Type</strong></td><td>The destination: <code>IP Address</code>, <code>Service Tag</code>, or <code>Application Security Group</code>.</td></tr><tr><td><strong>Destination Value</strong></td><td>IP/CIDR, Service tag, or ASG name for the destination.</td></tr><tr><td><strong>Destination Port Range</strong></td><td>Port or port range to allow/deny at the destination.</td></tr><tr><td><strong>Priority</strong></td><td>Rule priority. Lower values are higher priority (e.g., <code>100</code>, <code>200</code>).</td></tr><tr><td><strong>Protocol</strong></td><td>Choose <code>TCP</code>, <code>UDP</code>, or <code>Both</code>.</td></tr><tr><td><strong>Action</strong></td><td>Select <code>Allow</code> or <code>Deny</code> to permit or block the traffic.</td></tr></tbody></table>

5. Click **Add**. The Security Group Rule is configured.&#x20;

<div align="left"><figure><img src="../../../.gitbook/assets/image (7) (3).png" alt=""><figcaption><p><strong>Add Infrastructure Security</strong> pane</p></figcaption></figure></div>

