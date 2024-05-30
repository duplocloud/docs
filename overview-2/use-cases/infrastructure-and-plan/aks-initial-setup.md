---
description: Enable Azure Kubernetes Service (AKS) to connect with Azure
---

# AKS initial setup

## Enabling the AKS Kubernetes Cluster

Once your Infrastructure and Plan have been created, the final step before creating a Tenant is to enable Azure Kubernetes Service (AKS) to connect with Azure cloud management.

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**.
2. Select the Infrastructure that you created, in the **NAME** column of the Infrastructure page.
3. Click the **Kubernetes** tab. The following message displays: **Kubernetes cluster is not yet enabled. Click Here to enable the Kubernetes Cluster**.
4. Click on the **Click Here** hyperlink. The **Configure AKS Cluster** pane displays.
5. In the **Cluster name** field, specify a name for your cluster.
6. From the **AKS Version** item list, select your AKS version.
7. Select the correct plugin from the **Network Plugin** item list.
8.  Accept the default values for the remaining fields, and click **Create** to enable the AKS service for your Infrastructure. \


    <div align="left">

    <figure><img src="../../../.gitbook/assets/new reduced pic (1).png" alt=""><figcaption><p>The <strong>Configure AKS Cluster</strong> pane</p></figcaption></figure>

    </div>

DuploCloud begins creating and configuring an AKS cluster using Kubernetes. You receive an alert message when the Infrastructure has been updated.&#x20;

{% hint style="success" %}
It may take some time for enablement to complete. Use the **Kubernetes** card in the Infrastructure screen to monitor the status, which should display as **Enabled** when completed. You can also monitor progress by using the **Kubernetes** tab, as DuploCloud generates your **Cluster Name**, **Default VM Size**, **Server Endpoint**, and **Token**.&#x20;
{% endhint %}
