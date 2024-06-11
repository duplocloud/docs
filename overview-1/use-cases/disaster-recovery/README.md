---
description: Create an Infrastructure and Plan for GCP.
---

# Creating an Infrastructure and Plan for GCP

## Creating an Infrastructure

{% hint style="warning" %}
Up to one (0 or 1) GKS instance is supported for each DuploCloud Infrastructure.
{% endhint %}

1. Click **Administrator** -> **Infrastructure** from the navigation menu.&#x20;
2. Click **Add**.
3. Define the Infrastructure by completing the fields on the **Add Infrastructure** form.&#x20;
4. Optionally, click **Enable GKE** and complete the additional fields to [create a GKE Autopilot or Standard Cluster](creating-gke-autopilot-cluster.md).
5. Click **Create**. The Infrastructure is created and is listed on the **Infrastructure** page. DuploCloud automatically creates a [Plan ](../../../welcome-to-duplocloud/duplocloud-common-components/plan.md)with the same name and configuration as the Infrastructure.&#x20;

{% hint style="warning" %}
Cloud providers limit the number of Infrastructures that can run in each region. If you have completed the steps to create an Infrastructure and it doesn't show a status of Complete, try selecting a different region.&#x20;
{% endhint %}
