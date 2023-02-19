---
description: AWS-specific cloud provider deployments
coverY: 0
---

# Azure Overview

{% hint style="info" %}
Before you begin, read through the [DuploCloud Platform Overview](broken-reference) and are familiar with DuploCloud terms such as [Infrastructure](../getting-started/application-focussed-interface/infrastructure.md), [Plan](../getting-started/application-focussed-interface/plan.md), and [Tenant](../getting-started/application-focussed-interface/tenant.md).
{% endhint %}

The DuploCloud platform installs a Virtual Machine resource within your Azure Subscription. It can be accessed using a web interface, API, and a Terraform provider. Login to the DuploCloud portal via SSO, either through your GSuite or O365 login.&#x20;

## Prerequisites

Before you begin:

* Install the DuploCloud Portal and set up [Administrator and user access](../administrator-tools/access-control/).
* Connect to the DuploCloud Slack channel for support from the DuploCloud team. The support team is available to help you 24x7 with Slack and email support. We cover what is supported in the DuploCloud platform, as well as assist with your cloud provider's requirements.&#x20;

![DuploCloud Sample Architecture for Microsoft Azure](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F68cb0s9ce5UIUKWPuYs8%2Fuploads%2FENalQ7CcBZGkVhetVFi1%2Fimage.png?alt=media\&token=ff1c6622-f836-4938-ab0e-a0e36c95ce7e)

Behind the scenes, the topology that will get created will look like the following lower-level configuration in Azure.
