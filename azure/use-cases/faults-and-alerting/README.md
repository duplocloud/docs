---
description: Checking Faults and Alerts in the DuploCloud Portal
---

# Faults and alerts

## Introduction <a href="#id-0-toc-title" id="id-0-toc-title"></a>

Faults that happen in the system be it Infrastructure creation, Container deployments, or Application health checks can be tracked in the DuploCloud portal under Faults Menu.

## Viewing faults <a href="#id-1-toc-title" id="id-1-toc-title"></a>

You can look at Tenant specific faults under **Deployments > Faults** or all the faults in the system under **Admin > Faults**. In addition to notifying you about the faults, DuploCloud integrates with Sentry, which will send an Email alert for the fault and also acts as a single place to look at all the events.

![](<../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png>)

## Creating alerts

You can create Azure alerts for the resources from the DuploCloud portal. The supported resource has Alerts Tab. Click on Add. Metrics are listed as per the resource. Select the required Threshold and configure the Alerts.

Alerts can also be configured from the Diagnostics --> Alerts option.

<div align="left">

<img src="../../../.gitbook/assets/image (7) (4).png" alt="">

</div>

When the alert Threshold is crossed, a Fault is generated in the DuploCloud portal.

![](<../../../.gitbook/assets/image (36).png>)
