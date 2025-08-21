---
description: Enable Azure Kubernetes Service (AKS) to connect with Azure
---

# AKS initial setup

Once your Infrastructure and Plan have been created, the final step before creating a Tenant is to enable Azure Kubernetes Service (AKS) to connect with Azure cloud management.

## Enabling the AKS Kubernetes Cluster

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**.
2. Select the Infrastructure that you created from the **NAME** column.
3. Select the **Kubernetes** tab.&#x20;
4. Click on the **Click Here** link. The **Configure AKS Cluster** pane displays.

<div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (44).png" alt="" width="341"><figcaption></figcaption></figure></div>

5. Complete the following fields in the **Configure AKS Cluster** pane:

<table><thead><tr><th width="155.55560302734375">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Cluster Name</strong></td><td>Enter a unique name for the AKS cluster.</td></tr><tr><td><strong>Node VM Size</strong></td><td>Select the Azure VM size for the Kubernetes worker nodes (e.g., <strong>Standard_DS2_v2</strong>).</td></tr><tr><td><strong>AKS Version</strong></td><td>Select the desired Kubernetes version.</td></tr><tr><td><strong>Cluster Type</strong></td><td>Choose between:<br>• <strong>Public</strong>: Exposes the API server via public IP<br>• <strong>Private</strong>: Restricts access to the cluster within the virtual network</td></tr><tr><td><strong>Node Count</strong></td><td>Specify the number of nodes to deploy in the system node pool.</td></tr><tr><td><strong>Max Pods</strong></td><td>Set the maximum number of pods that can run on each node. Increasing this allows more pods per node but can affect node performance. Defaults depend on VM size.</td></tr><tr><td><strong>System NodePool Autoscaling</strong></td><td>Optionally, enable autoscaling for the system node pool and specify the minimum and maximum number of nodes. DuploCloud will automatically scale the node count within this range based on workload demand.</td></tr></tbody></table>

6. Optionally, select **Advanced Options.**

<div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (45).png" alt=""><figcaption><p>The <strong>Advanced Options</strong> section of the <strong>Configure AKS Cluster</strong> pane</p></figcaption></figure></div>

7. Complete the following fields.&#x20;

<table data-header-hidden><thead><tr><th width="194.66668701171875">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Network Plugin</strong></td><td>Select the Kubernetes network plugin:<br>• <strong>Azure</strong>: Integrates AKS networking with Azure VNETs (recommended)<br>• <strong>Kubenet</strong>: Basic plugin with limited Azure network integration</td></tr><tr><td><strong>K8s Resource Group</strong></td><td>Optionally, enter the name of an existing Azure resource group to associate with the AKS cluster. If left blank, DuploCloud creates a dedicated resource group automatically.</td></tr><tr><td><strong>Outbound Connectivity</strong></td><td>Select how outbound internet traffic from the AKS cluster is routed:<br>• <strong>Load Balancer</strong>: Outbound traffic goes through a standard Azure public load balancer.<br>• <strong>User Defined Routing:</strong> Outbound traffic is routed via custom Azure route tables you configure.</td></tr></tbody></table>

7. Click **Create** to enable AKS for your Infrastructure. DuploCloud begins creating and configuring an AKS cluster using Kubernetes. You receive an alert message when the Infrastructure has been updated.&#x20;

{% hint style="success" %}
It may take some time to configure the cluster. The **Kubernetes** card on the Infrastructure page shows **Enabled** when the cluster is complete. You can also monitor progress using the **Kubernetes** tab.
{% endhint %}
