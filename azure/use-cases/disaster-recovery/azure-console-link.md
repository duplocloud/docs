---
description: Create a link to the Azure Console from DuploCloud
---

# Azure Console link

Creating a direct link to the Azure Portal from your DuploCloud Infrastructure saves you time when you work with DuploCloud Azure Hosts. Instead of toggling between the DuploCloud Portal and the Microsoft Azure Portal, get instant access to the Azure Portal from DuploCloud.

## Creating a link to the Azure Console&#x20;

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**. The **Infrastructure** page displays.
2. From the **Name** column, select the Infrastructure for which you want to add a link to the Azure Console.
3. Click the **Metadata** tab.
4. Click **Add**. The **Add Infrastructure Tag** pane displays.
5.  In the **Key** field, enter **AzurePortalLink**.

    <figure><img src="../../../.gitbook/assets/azure_portal.png" alt=""><figcaption><p><strong>Add infrastructure Tag</strong> pane with <strong>Key AzurePortalLink</strong></p></figcaption></figure>
6. In the **Value** field, enter the URL for your Azure Portal.&#x20;
7. Click **Create**.

{% hint style="warning" %}
The **Value** in the example above is DuploCloud's internal Azure Portal link.
{% endhint %}

## Accessing the Azure Console

After you [create a link to the Azure Console](azure-console-link.md#creating-a-link-to-the-azure-console) from an Infrastructure, access the Azure Console from the DuploCloud Portal in the **Actions** menu for Azure **Hosts**.

1. In the DuploCloud Portal, navigate to **DevOps** -> **Hosts**. The **Hosts** page displays.
2. From the **Name** column, select the Host you are working with.
3. From the **Actions** menu, select **Azure Portal**.

<figure><img src="../../../.gitbook/assets/aws-con_app.png" alt=""><figcaption><p><strong>HOST1</strong> host page with <strong>Action Menu</strong> displaying <strong>Azure Portal</strong> link</p></figcaption></figure>
