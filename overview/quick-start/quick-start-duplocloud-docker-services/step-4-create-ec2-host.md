---
description: Create an EC2 Host in DuploCloud
---

# Step 4: Create an EC2 Host

Before you create your application and service using native Docker, create an EC2 Host for storage in DuploCloud.

_Estimated time to complete Step 4: 5 minutes._

## Prerequisites

Before creating a Host (essentially a [Virtual Machine](https://en.wikipedia.org/wiki/Virtual\_machine)), verify that you accomplished the tasks in the previous tutorial steps. Using the DuploCloud Portal, confirm that:

* An [Infrastructure and Plan](../step-1-infrastructure.md) exist, both with the name **NONPROD**.
* A Tenant with the name [**dev01** has been created](../step-2-tenant.md).

### Select the Tenant you created

In the **Tenant** list box, on the upper-left side of the DuploCloud Portal, select the **dev01** Tenant that you created.

<div align="left">

<figure><img src="../../../.gitbook/assets/tenant_dev01 (6).png" alt=""><figcaption><p><strong>Tenant</strong> list box in the DuploCloud Portal</p></figcaption></figure>

</div>

## Creating a host

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Hosts**. The **Hosts** page displays.
2. In the **EC2** tab, click **Add**. The **Add Hosts** page displays.
3. In the **Friendly Name** field, enter **host01**.
4. From the **Instance Type** list box, select **2 CPU 4 GB - t3.medium**.
5. Select the **Advanced Options** checkbox to display advanced configuration fields.
6. From the **Agent Platform** list box, select **Linux/Docker Native**.
7. From the **Image ID** list box, select any **Docker-Duplo** or **Ubuntu** image. &#x20;
8. Click **Add**. The Host is created, initialized, and started. In a few minutes, when the **Status** displays **Running**, the Host is available for use.

<figure><img src="../../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.17-17_39_57.png" alt=""><figcaption><p><strong>EC2 Add Hosts</strong> page</p></figcaption></figure>

## Checking your work

Verify that **host01** has a **Status** of **Running**.

<figure><img src="../../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.17-18_05_17.png" alt=""><figcaption><p><strong>EC2</strong> tab displaying <strong>host01</strong> with <strong>Status</strong> of <strong>Running</strong></p></figcaption></figure>
