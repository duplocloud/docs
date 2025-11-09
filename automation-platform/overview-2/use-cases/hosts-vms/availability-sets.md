---
description: Configure Azure Availability Sets in DuploCloud
---

# Availability Sets

Azure Availability Sets enhance the high availability and fault tolerance of virtual machines (VMs) deployed within Azure. They distribute VMs across multiple fault and update domains to protect against hardware failures and reduce downtime during maintenance events.

In DuploCloud, Availability Sets can be configured when creating or managing hosts. There are two types of Availability Sets:

* **Aligned Availability Set**: Used for VMs with **managed disks** and provides better fault domain management.
* **Classic Availability Set**: Used for VMs with **unmanaged disks** and follows older Azure infrastructure standards.

## Creating an Availability Set in DuploCloud

1. Select the Tenant from the **Tenant** list box.&#x20;
2. Navigate to **Cloud Services** -> **Hosts.**
3. Select the **Availability Set** tab, and click **Add**. The **Add Azure Availability Set** pane displays.

<div align="left"><figure><img src="../../../../.gitbook/assets/Availability Set (1).png" alt="" width="375"><figcaption><p>The <strong>Add Azure Availability Set</strong> pane</p></figcaption></figure></div>

4. Fill in the following details:
   * **Name**: Enter a descriptive name for the Availability Set.
   * **Use managed disks**: Select whether to use **Managed** (recommended) or **Classic** disks.
   * **Platform Fault Domain Count**: Specify the number of fault domains (up to 3 in most Azure regions).
   * **Platform Update Domain Count**: Specify the number of update domains (default is 5, max is 20).
5. Click **Add** to create the Availability Set.

<figure><img src="../../../../.gitbook/assets/AS success.png" alt=""><figcaption></figcaption></figure>

## Assigning an Availability Set to a Host

When [creating a new host](./), you can assign an Availability Set by selecting it from the **Availability Set** list box.

## Deleting an Availability Set

1. Select the Tenant from the **Tenant** list box.&#x20;
2. Navigate to **Cloud Services** -> **Hosts.**
3. Select the **Availability Set** tab.
4. Click the menu icon (<img src="../../../../.gitbook/assets/image (460).png" alt="" data-size="line">) on the left side of the row for the Availability Set, and select **Delete**.&#x20;
