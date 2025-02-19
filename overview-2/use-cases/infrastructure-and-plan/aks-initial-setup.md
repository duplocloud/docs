---
description: Enable Azure Kubernetes Service (AKS) to connect with Azure
---

# AKS initial setup

## Enabling the AKS Kubernetes Cluster

Once your Infrastructure and Plan have been created, the final step before creating a Tenant is to enable Azure Kubernetes Service (AKS) to connect with Azure cloud management.

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**.
2. Select the Infrastructure that you created from the **NAME** column.
3. Select the **Kubernetes** tab. The following message displays: **Kubernetes cluster is not yet enabled. Click Here to enable the Kubernetes Cluster**.
4. Click on the **Click Here** hyperlink. The **Configure AKS Cluster** pane displays.
5. \


<div align="left"><figure><img src="../../../.gitbook/assets/config AKS cluster (2).png" alt=""><figcaption></figcaption></figure></div>

1. In the **Cluster name** field, specify a name for your cluster.
2. Select your node VM size from the **Node VM Size** list box.&#x20;
3. From the **AKS Version** item list, select your AKS version.
4. In the **Cluster Type** item list, select **Public** or **Private**.
5. Optionally, select **Advanced Options** to specify your network plugin (**Azure** or **Kubenet**), K8s resource group field, and outbound connectivity source (**Load Balancer** or **User Defined Routing**).
6. Click **Create** to enable AKS for your Infrastructure.&#x20;

DuploCloud begins creating and configuring an AKS cluster using Kubernetes. You receive an alert message when the Infrastructure has been updated.&#x20;

{% hint style="success" %}
It may take some time to configure the cluster. The **Kubernetes** card on the Infrastructure page shows **Enabled** when the cluster is complete. You can also monitor progress using the **Kubernetes** tab.
{% endhint %}
