---
description: Using DuploCloud with Google Cloud Platform
coverY: 0
---

# GCP Overview

The DuploCloud platform installs a Virtual Machine resource within your GCP Project. It can be accessed using a web interface, API, and a Terraform provider. Log in to the DuploCloud portal via SSO through your GSuite or O365 login.&#x20;

{% hint style="info" %}
Read through the [DuploCloud Platform Overview](../) and are familiar with DuploCloud terms such as [Infrastructure](../getting-started/application-focussed-interface/infrastructure.md), [Plan](../getting-started/application-focussed-interface/plan.md), and [Tenant](../getting-started/application-focussed-interface/tenant/).
{% endhint %}

## Prerequisites

Before you begin, ensure that:

* DuploCloud Portal has been set up and you have access to it.
* You have access to your individual Slack or Teams channel for 24x7 support from the DuploCloud team.

Behind the scenes, a topology is created similar to the following low-level configuration in GCP.

<figure><img src="../.gitbook/assets/GCP_Rough_Top.png" alt=""><figcaption><p>DuploCloud Sample Architecture for GCP</p></figcaption></figure>
