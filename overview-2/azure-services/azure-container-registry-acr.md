---
description: Using Azure Container Registry for storage with DuploCloud
---

# Azure Container Registry (ACR)

[Azure Container Registry (ACR)](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-intro) is a fully managed Docker container registry that allows you to store and manage private container images in Azure. ACR provides a central repository for containerized applications, enabling seamless integration with Azure Kubernetes Service (AKS), Azure App Service, and other container-based services.

## Creating an Azure Container Registry

1. Select the appropriate Tenant from the **Tenant** list box.&#x20;
2. Navigate to **Cloud Services** -> **Storage**.
3. Select the **Container Registry** tab.
4.  Click **Add**. The **Create Container Registry** pane displays.<br>

    <div align="left"><figure><img src="../../.gitbook/assets/container registry.png" alt=""><figcaption><p>The <strong>Create Container Registry</strong> pane</p></figcaption></figure></div>
5. Complete the following fields:

<table data-header-hidden><thead><tr><th width="218.4444580078125"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the container registry.</td></tr><tr><td><strong>Tier</strong></td><td>Select the subscription tier e.g., <strong>Basic</strong>, <strong>Standard, Premium</strong>.</td></tr><tr><td><strong>Admin User Enabled</strong></td><td>Check this box to enable admin access.</td></tr><tr><td><strong>Anonymous Pull Enabled</strong></td><td>Check this box to allow anonymous pull access.</td></tr><tr><td><strong>Data Endpoint Enabled</strong></td><td>Check this box to enable a data endpoint for additional storage (<strong>Premium</strong> tier only).</td></tr><tr><td><strong>Public Network Access</strong></td><td>Choose to <strong>Enable</strong> or <strong>Disable</strong> public network access.</td></tr></tbody></table>

6. Click **Submit** to create the Azure Container Registry.

## Viewing Azure Container Registries

1. Select the appropriate Tenant from the **Tenant** list box.
2. Navigate to **Cloud Services** -> **Storage**.
3. Select the **Container Registry** tab to view a list of Container Registries.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot (735).png" alt=""><figcaption><p>The <strong>Container Registry</strong> tab in the DuploCloud Portal</p></figcaption></figure>
