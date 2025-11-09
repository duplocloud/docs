---
description: Grant AIM permissions to view billing data in Azure
---

# Enabling Azure Billing Data

To enable the billing feature in DuploCloud for Microsoft Azure, you must assign the **Billing Reader** role to the DuploCloud master VM (`DuploMaster`), restart the VM to apply the change, verify that the billing service is running, and then enable billing in the DuploCloud Portal.

## Step 1. Assign the Billing Reader Role

Follow the Azure documentation to [assign a role using the Azure portal](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-assignments-portal).

When assigning the role:

* **Scope**: Assign the role to the VM named **`DuploMaster`**.
* **Role**: Select **Billing Reader**.
* **Identity**: Choose the system-assigned or user-assigned managed identity associated with the VM.

{% hint style="info" %}
To locate the DuploMaster VM, go to Azure Virtual Machines and search for a name beginning with `DuploMaster`.
{% endhint %}

## Step 2. Restart the VM

After assigning the role, restart the `DuploMaster` VM so the role assignment takes effect.

Refer to [Restart a virtual machine in Azure](https://learn.microsoft.com/en-us/azure/virtual-machines/windows/restart) for detailed instructions.

## Step 3. Enable Billing in DuploCloud

To complete the setup:

1. From the DuploCloud Portal, navigate to **Administrator > Billing**.
2.  On the right side of the page, click **Enable Billing Feature**.\


    <figure><img src="../../../../.gitbook/assets/Screenshot (600) (6).png" alt=""><figcaption></figcaption></figure>

Billing data will be displayed as it becomes available from Azure.
