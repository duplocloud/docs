---
description: DuploCloud Tenants and Security Groups
---

# Security Groups

In DuploCloud, each Tenant is associated with its own Security Group, which allows unrestricted communication between all resources within that Tenant. This setup ensures that any computing resource in that Tenant can easily reach the services within that same Tenant.

## Adding Security Rules for a Tenant

You can configure security rules for a Tenant to control which traffic is allowed to reach resources within it. This includes both IPv4 and IPv6 addresses, VPN clients, or traffic from other Tenants.

1. Navigate to **Administrator** -> **Tenants**.
2. Select the Tenant from the **NAME** column.
3. Select the **Security** tab.&#x20;
4.  Click **Add**. The **Add Tenant Security** pane displays.<br>

    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (928).png" alt="" width="365"><figcaption><p><strong>Add Tenant Security</strong> pane</p></figcaption></figure></div>
5. Complete the following fields:

<table data-header-hidden><thead><tr><th width="171.111083984375">Field</th><th>Description (What the user does)</th></tr></thead><tbody><tr><td><strong>Source Type</strong></td><td>Select <strong>Tenant</strong> to allow access from another DuploCloud Tenant, or <strong>IP Address</strong> to allow traffic from a specific IP or VPN range.</td></tr><tr><td><strong>Tenant</strong></td><td>If <strong>Source Type = Tenant</strong>, select the Tenant you want to allow access from.</td></tr><tr><td><strong>IP CIDR</strong></td><td>If <strong>Source Type = IP Address</strong>, select <strong>Custom</strong> to manually enter an IP or CIDR (IPv4 or IPv6), or <strong>VpnIp</strong> to allow access from VPN clients.</td></tr><tr><td><strong>Protocol</strong></td><td>Choose the protocol for the rule: <strong>TCP</strong>, <strong>UDP</strong>, or <strong>ICMP</strong>.</td></tr><tr><td><strong>Port Range</strong></td><td>If the protocol is TCP or UDP, specify the port range (for example, 1-65535).</td></tr><tr><td><strong>Description</strong></td><td>Optionally, add a note describing the purpose of the rule.</td></tr></tbody></table>

6. Click **Add** to save the Security rule.&#x20;

### Allowing Inter-Tenant Access

To enable traffic between two DuploCloud Tenants, you create a Tenant security group rule:

1. Follow the steps in Adding Security Group Rules for a Tenant to open the Add Tenant Security pane.
2. In **Source Type**, select **Tenant**.
3. In **Tenant**, select the Tenant you want to allow access from.
4. Configure **Protocol** and **Port Range** as needed.
5. Optionally, enter a **Description** for the rule.
6. Click **Add**. This rule allows all resources in the selected source Tenant to communicate with resources in the current Tenant according to the ports and protocol you specified.

### **Configuring Azure VNet Security**

In Azure, security is implemented at the **Virtual Network (VNet)** level. All traffic within the VNet is allowed by default. However, Administrators can override this behavior by setting up security rules to control traffic between different VNets or from a VNet to external resources.

1. From the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**.
2. Select the Infrastructure you want to manage access for from the **NAME** column.
3. Select the **Security Group Rules** tab.&#x20;
4.  Click **Add**. The **Add Infrastructure Security** pane displays.<br>

    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (327).png" alt=""><figcaption><p>The <strong>Add Infrastructure Security</strong> pane</p></figcaption></figure></div>
5. Complete the fields:

<table data-header-hidden><thead><tr><th width="175.77777099609375"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>A unique name for the rule.</td></tr><tr><td><strong>Subnet</strong></td><td>The subnet this rule will apply to (e.g., <code>custom-default</code>).</td></tr><tr><td><strong>Direction</strong></td><td>Whether the rule applies to <code>Inbound</code> or <code>Outbound</code> traffic.</td></tr><tr><td><strong>Source Type</strong></td><td>The source of the traffic: <code>IP Address</code>, <code>Service Tag</code>, or <code>Application Security Group</code>.</td></tr><tr><td><strong>Source Value</strong></td><td>IP/CIDR (e.g., <code>10.0.0.0/8</code>), service tag (e.g., <code>Internet</code>), or ASG name.</td></tr><tr><td><strong>Source Port Range</strong></td><td>Port or port range from the source (e.g., <code>*</code>, <code>443</code>, <code>1000-2000</code>).</td></tr><tr><td><strong>Destination Type</strong></td><td>The destination: <code>IP Address</code>, <code>Service Tag</code>, or <code>Application Security Group</code>.</td></tr><tr><td><strong>Destination Value</strong></td><td>IP/CIDR, Service tag, or ASG name for the destination.</td></tr><tr><td><strong>Destination Port Range</strong></td><td>Port or port range to allow/deny at the destination.</td></tr><tr><td><strong>Priority</strong></td><td>Rule priority. Lower values are higher priority (e.g., <code>100</code>, <code>200</code>).</td></tr><tr><td><strong>Protocol</strong></td><td>Choose <code>TCP</code>, <code>UDP</code>, or <code>Both</code>.</td></tr><tr><td><strong>Action</strong></td><td>Select <code>Allow</code> or <code>Deny</code> to permit or block the traffic.</td></tr></tbody></table>

5. Click **Add**. The Security Group Rule is configured.&#x20;
