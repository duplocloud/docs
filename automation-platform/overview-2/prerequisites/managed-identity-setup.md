---
description: Configure managed identity for the DuploCloud Portal in Azure.
---

# Managed Identity Setup

Managed Identity (MI) in Azure allows DuploCloud to authenticate securely to Azure services without managing credentials. DuploCloud requires the VM where it is installed to have owner access to the Azure subscription to launch and manage Azure resources effectively. To enable this, configure a MI in Azure for DuploCloud.&#x20;

## Step 1: Create a Managed Identity in Azure

1. Log in to the Azure Portal.
2. Navigate to **Managed Identities**.
3. Click on **+** **Add** to create a new managed identity.
4. Fill the fields:

<table data-header-hidden><thead><tr><th width="156.22222900390625"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a meaningful name for the managed identity (e.g., <code>duplo-master-managed-identity</code>).</td></tr><tr><td><strong>Subscription</strong></td><td>Select the subscription where the identity will be created.</td></tr><tr><td><strong>Resource Group</strong></td><td>Choose an existing resource group or create a new one.</td></tr><tr><td><strong>Region</strong></td><td> Select the appropriate region for the managed identity</td></tr><tr><td></td><td></td></tr></tbody></table>

5. Click **Create** and wait for the deployment to complete.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Create a managed identity</p></figcaption></figure>

## Step 2: Assign the Managed Identity to Duplo-Master VM

1. Go to **Virtual Machines** in the Azure portal and select the VM where DuploCloud is installed.
2.  Under the **Security** section, select **Identity**.\


    <figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption><p>Assigning managed identity to the Duplo-Master VM</p></figcaption></figure>
3. Select the **User assigned** tab and click **+** **Add**.
4. Select the managed identity created in Step 1, and click **Add**.

## Step 3: Assign Owner Role to the Managed Identity

1. Go to **Subscriptions** in the Azure portal, and select the subscription where resources will be launched by DuploCloud.
2.  Under **Access Control (IAM)**, click **+ Add** -> **Add role assignment**.\


    <figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Role assignment for Managed Identity</p></figcaption></figure>
3. Select the **Privileged administrator roles** tab
4. Select **Owner** in the **Role** list box.&#x20;
5. In the **Assign access to** field, choose **Managed identity**.
6. Search for and select the managed identity created in Step 1.
7. Click **Save** to complete the role assignment.

## Step 4: Assign Owner Role to the DuploCloud VM

1. Go to **Subscriptions** in the Azure portal.
2. Select the subscription where resources will be launched by DuploCloud.
3.  Under **Access Control (IAM)**, click **+ Add** -> **Add role assignment**.\


    <figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Role assignment for VM</p></figcaption></figure>
4. Select the **Privileged administrator roles** tab
5. Select **Owner** in the **Role** list box.
6. In the **Assign access to** field, choose **Managed Identity**.
7. Search for and select the DuploCloud VM.
8. Click **Save** to apply the changes.

## Additional Notes

* Ensure that both the managed identity and the VM are in the same subscription where resources will be launched.
* Verify the assignments under **Access Control (IAM)** for both the managed identity and the VM to ensure correct configurations.
