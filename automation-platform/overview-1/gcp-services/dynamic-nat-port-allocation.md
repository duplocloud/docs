---
description: Enable dynamic NAT port allocation in GCP
---

# Dynamic NAT Port Allocation

Dynamic NAT Port Allocation allows instances in private subnets to initiate outbound connections while efficiently managing port usage. Instead of assigning a fixed port range per instance, this feature dynamically distributes port allocation across the infrastructure.

When enabled, DuploCloud configures GCP to allocate NAT ports dynamically to instances that require outbound internet access. This reduces the number of required external IP addresses and improves scalability in NATed environments.

This feature is especially useful for:

* Highly dynamic workloads.
* Tenants running many lightweight services that occasionally connect to the internet.

## Enabling Dynamic NAT Port Allocation

To enable Dynamic NAT port allocation for a DuploCloud Infrastructure:

1. In the DuploCloud Portal, navigate to **Administrator** → **Infrastructure**.
2. Select the GCP infrastructure you want to configure from the **NAME** column.
3. Select the **Settings** tab.
4.  Click **Add**. The **Infra - Set Custom Data** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (659).png" alt=""><figcaption><p><strong>Infra - Set Custom Data</strong> pane</p></figcaption></figure></div>
5. In the **Setting Name** field, select **Enable Dynamic NAT Port Allocation** from the list box.
6. Select **Enable**.
7. Click **Set**. Dynamic NAT Port Allocation is enabled.
