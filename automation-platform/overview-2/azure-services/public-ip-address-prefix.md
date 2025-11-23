---
description: Use a Public IP Address to reserve a range of consecutive public IPs
---

# Public IP Address Prefix

A [Public IP Address Prefix](https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/public-ip-address-prefix) reserves a range of consecutive public IP addresses that you can individually assign to public resources. This is useful for scaling because it provides a globally unique address space, supports expansion across locations, facilitates load balancing, enables secure access control, and is fundamental for connecting to multiple ISPs and participating in internet routing protocols.

## Adding a Public IP Address Prefix

1. Select the correct **Tenant** from the Tenant list in the upper left.
2. In the DuploCloud Portal, navigate to **Cloud Services** -> **App Integration**.&#x20;
3.  Click on the **Public IP Prefix** tab.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (223).png" alt=""><figcaption><p>The <strong>Public IP Prefix</strong> tab.</p></figcaption></figure>
4. Click **Add**. The **Add Public IP Prefix** pane displays.
5.  In the **Name** field, enter a name. Select your desired length (number of addresses) from the **Prefix Length** item list. Select the resource type from the **Resource Type** item list.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/add prefix (1).png" alt="" width="362"><figcaption><p>The <strong>Add Public IP Prefix</strong> pane.</p></figcaption></figure></div>
6. Click **Add**. Your **Public IP Prefix** is created.&#x20;

