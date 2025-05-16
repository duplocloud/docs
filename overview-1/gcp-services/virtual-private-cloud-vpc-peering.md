---
description: Establish communication between GCP VPCs via VPC peering
---

# Virtual Private Cloud (VPC) Peering

Virtual Private Cloud (VPC) peering establishes a direct networking connection between two VPCs, allowing traffic to flow seamlessly between them. With VPC peering, resources in the connected VPCs can communicate as though they are part of the same network, even if the VPCs reside in different regions (referred to as Inter-Region VPC peering).

This connection is ideal for facilitating data transfer between environments. For instance, if you manage multiple GCP projects, you can peer the VPCs across those projects to enable secure communication and resource sharing, such as setting up a file-sharing network.

## Setting Up VPC Peering in DuploCloud

To set up VPC peering in DuploCloud, first configure peering in the source Infrastructure, then confirm peering in the destination Infrastructure.&#x20;

### Configure peering in the source Infrastructure

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**.
2. In the **NAME** column, select the name of the source Infrastructure.&#x20;
3. Select the **Peering** tab.
4.  Click **Add**. The **Create VPC Peering** pane displays. \


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (8).png" alt="" width="388"><figcaption><p>The <strong>Create VPC Peering</strong> pane</p></figcaption></figure></div>
5. Select the **Destination Infrastructure**.&#x20;
6. Optionally, enable **Bi-Direction/Duplex Peering**, **Export Custom Routes**, **Import Custom Routes**, **Export Subnets Routes With Public IP**, or **Import Subnet Routes With Public IP**. Complete additional fields/selections as required.
7. Click **Create**. VPC peering is configured.&#x20;

### Confirm peering in the destination Infrastructure

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**.
2. In the **NAME** column, select the name of the destination Infrastructure.&#x20;
3. Select the **Peering** tab.
4. In the row of the peering connection, click the menu icon (<img src="../../.gitbook/assets/menu icon.webp" alt="" data-size="line">).&#x20;
5. Select **Edit**. The **Update VPC Peering** pane displays.
6. Click **Update**. Verify that the peering status is **Active**.&#x20;

<figure><img src="../../.gitbook/assets/active peering.png" alt=""><figcaption></figcaption></figure>
