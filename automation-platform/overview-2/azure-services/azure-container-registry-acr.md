---
description: Using Azure Container Registry for storage with DuploCloud
---

# Azure Container Registry (ACR)

[Azure Container Registry (ACR)](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-intro) is a fully managed Docker container registry that allows you to store and manage private container images in Azure. ACR provides a central repository for containerized applications, enabling seamless integration with Azure Kubernetes Service (AKS), Azure App Service, and other container-based services.

## Configuring Azure Container Registry in DuploCloud

1. Select the appropriate Tenant from the **Tenant** list box.&#x20;
2. Navigate to **Cloud Services** -> **Storage**.
3. Select the **Container Registry** tab.
4.  Click **Add**. The **Create Container Registry** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/container registry.png" alt="" width="366"><figcaption><p>The <strong>Create Container Registry</strong> pane</p></figcaption></figure></div>
5. In the **Name** field, enter a name for the registry.&#x20;
6. Select the desired tier (**Basic**, **Standard**, or **Premium**) from the **Tier** list box.&#x20;
7. Optionally, enable the following:
   * **Admin User Enabled**: Grants administrative access.
   * **Anonymous Pull Enabled**: Allows anonymous access for pulling images.
   * **Data Endpoint Enabled** (Premium tier only): Enables data endpoint for additional storage.
8. Enable or disable **Public Network Access**, as needed.&#x20;
9. Click **Submit**. DuploCloud creates the Azure Container Registry with the specified settings and makes it available for use.

## Viewing Azure Container Registries

Select the appropriate Tenant from the **Tenant** list box and navigate to the **Container Registry** tab (**Cloud Services** -> **Storage** -> **Container Registry**) to view your container registry details and statuses.&#x20;

<figure><img src="../../../.gitbook/assets/container registry success (1).png" alt=""><figcaption><p>The <strong>Container Registry</strong> tab in the DuploCloud Portal</p></figcaption></figure>
