---
description: Using DuploCloud with Microsoft Azure
cover: ../.gitbook/assets/Linkedin-bannerV2 (1).png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Azure User Guide

The DuploCloud platform installs a Virtual Machine resource within your Azure Subscription. It can be accessed using a web interface, API, or a Terraform provider. Login to the DuploCloud Portal via SSO  through your GSuite or O365 login.&#x20;

{% hint style="info" %}
Read through the [DuploCloud Platform Overview](../) and learn about DuploCloud terms such as [Infrastructure](../welcome-to-duplocloud/application-focussed-interface/duplocloud-common-components/infrastructure.md), [Plan](../welcome-to-duplocloud/application-focussed-interface/duplocloud-common-components/plan.md), and [Tenant](../welcome-to-duplocloud/application-focussed-interface/duplocloud-common-components/tenant.md).
{% endhint %}

## Prerequisites

Before you begin, ensure that:

* DuploCloud Portal has been set up and you have access to it.
* You have access to your individual Slack channel for 24x7 support from the DuploCloud team.

Behind the scenes, a topology is created similar to the following low-level configuration in Azure.

![DuploCloud Sample Architecture for Microsoft Azure](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F68cb0s9ce5UIUKWPuYs8%2Fuploads%2FENalQ7CcBZGkVhetVFi1%2Fimage.png?alt=media\&token=ff1c6622-f836-4938-ab0e-a0e36c95ce7e)
