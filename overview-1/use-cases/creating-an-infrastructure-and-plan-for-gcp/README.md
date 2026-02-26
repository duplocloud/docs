---
description: >-
  Use the DuploCloud Portal to create an Infrastructure and associated Plan for
  GCP
---

# Creating an Infrastructure and Plan for GCP

A GCP Infrastructure in DuploCloud sets up the networking and environment needed to deploy resources in Google Cloud. You can also choose to include a GKE (Google Kubernetes Engine) cluster.

Each GCP Infrastructure can include up to one GKE cluster, using either Autopilot (fully managed by Google) or Standard (manually managed).

When the infrastructure is created, DuploCloud automatically creates a Plan with the same name.

## Creating an Infrastructure

1. Navigate to **Administrator** -> **Infrastructure**.&#x20;
2.  Click **Add**. The **Add Infrastructure** pane displays.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (661).png" alt=""><figcaption></figcaption></figure>
3. Complete the following fields to define the infrastructure.&#x20;

<table data-header-hidden><thead><tr><th width="196.22216796875"></th><th></th></tr></thead><tbody><tr><td><br><strong>Name</strong></td><td>Enter a name for the infrastructure.</td></tr><tr><td><strong>Cloud</strong></td><td>Select the cloud provider. <strong>Google</strong> is selected by default.</td></tr><tr><td><strong>VPC CIDR</strong></td><td>Enter the CIDR block for the VPC (e.g., <code>10.10.0.0/16</code>).</td></tr><tr><td><strong>Region</strong></td><td>Select the GCP region to deploy into.</td></tr><tr><td><strong>Account</strong></td><td>Specify the GCP account to use for this infrastructure.</td></tr><tr><td><strong>Subnet CIDR Bits</strong></td><td>Enter the number of bits to define the size of each subnet.</td></tr><tr><td><strong>Enable GKE</strong></td><td>Check this box to include a GKE cluster.</td></tr></tbody></table>

4. If you selected **Enable GKE**, complete the following fields.

<table data-header-hidden><thead><tr><th width="237.99993896484375"></th><th></th></tr></thead><tbody><tr><td><strong>Cluster Mode</strong></td><td>Choose <strong>GKE Autopilot</strong> or <strong>GKE Standard</strong>.</td></tr><tr><td><strong>Release Channel</strong></td><td><p>Specify the GKE release channel to control the frequency and stability of cluster updates. </p><ul><li><strong>Rapid</strong>: Get the latest GKE features as soon as they’re available.</li><li><strong>Regular</strong> <strong>(recommended)</strong>: Balanced feature updates and stability.</li><li><strong>Stable</strong>: Emphasizes long-term stability with fewer updates.</li><li><strong>Extended</strong>: For workloads that require extended maintenance and support for older versions.</li></ul></td></tr><tr><td><strong>GKE Version</strong></td><td>Select the Kubernetes version to use. A default version will be pre-selected based on the release channel, but you can manually choose a different supported version if needed.</td></tr><tr><td><strong>GKE Endpoint Visibility</strong></td><td>Choose whether the Kubernetes API endpoint is public or private.</td></tr><tr><td><strong>Cluster IP CIDR</strong></td><td>Enter the internal CIDR block for the cluster.</td></tr><tr><td><strong>Disable NAT Creation</strong></td><td>Check this box to stop DuploCloud from creating a Cloud NAT gateway. </td></tr></tbody></table>

5. Click **Create**. The Infrastructure is created and is listed on the **Infrastructure** page. DuploCloud automatically creates a [Plan](../../../automation-platform/application-focused-interface-duplocloud-architecture/plan.md#duplocloud-plans) with the same name and configuration as the Infrastructure.

{% hint style="info" %}
Cloud providers limit the number of Infrastructures that can run in each region. If you have completed the steps to create an Infrastructure and it doesn't show a status of **Complete**, check logs on GCP Console for any errors or contact DuploCloud Support.
{% endhint %}
