---
description: Using DuploCloud Tenants for Azure
---

# Creating a Tenant (Environment)

In Azure, Microsoft cloud features such as Azure resource groups, Azure managed identity, Azure application security groups (ASG), KMS keys, and Kubernetes Namespaces are exposed in Tenants which reference their configurations.

For more information about DuploCloud Tenants, see the [Tenants](../../../application-focused-interface-duplocloud-architecture/tenant.md) topic in the Getting Started with DuploCloud section.&#x20;

## Creating a Tenant <a href="#id-2-toc-title" id="id-2-toc-title"></a>

1.  Navigate to **Administrator** -> **Tenant** in the DuploCloud Portal and click **Add**. The **Create a Tenant** pane displays.<br>

    <div align="left"><figure><img src="../../../../.gitbook/assets/image (5) (2).png" alt="" width="404"><figcaption><p><strong>Create a Tenant</strong> pane</p></figcaption></figure></div>
2. In the **Name** field, enter a name for the Tenant. Choose unique names that are not substrings of one another, for example, if you have a Tenant named `dev`, you cannot create another named `dev2`. We recommend using distinct numerical suffixes like `dev01` and `dev02`.
3. In the **Plan** list box, select the Plan to associate the Tenant with.&#x20;
4. Click **Create**. The Tenant is created.&#x20;
