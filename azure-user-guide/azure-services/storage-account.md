# Storage account

DuploCloud Azure Portal provides the ability to create Storage Accounts, File Shares, and generate Shared Access Signatures (SAS). Storage Accounts with a SKU Type `Standard_LRS` are created. Users can view additional details of File Share endpoints from the Portal.

### Create Storage Account

Navigate to **DevOps** > **Storage Account** to create Storage Account.

Provide unique name to create Storage Account.

<div align="left">

<img src="../../.gitbook/assets/image (54).png" alt="Add Storage Account screen">

</div>

### View Storage Account

You can view Storage Account Details once created. You can view Endpoint details in the Storage Account table view.\
Click on the  <img src="../../.gitbook/assets/image (1) (1) (2).png" alt="" data-size="line">icons under the Actions Column to view and copy the keys of the Storage Account.

![Storage Account Details Screen](<../../.gitbook/assets/image (23) (2).png>)

### Create and View File Shares

Create File Shares by clicking on **Add**.&#x20;

![View File Share](<../../.gitbook/assets/image (33).png>)

### Generate Shared Access Signature (SAS)

Click on **Actions** > **Shared Access Signature**. Provide access details in the screen below. Review and generate Shared Access Signature(SAS) tokens.

<div align="left">

<img src="../../.gitbook/assets/image (28).png" alt="">

</div>

Once Signature Tokens are generated, Azure user can copy paste the token and URL's in a secure location. They'll only be displayed once and cannot be retrieved once the window is closed.

### Block Public Access to Storage Accounts

You can configure the **Tenant** to block public network access to **Storage Accounts.**

1. From the DuploCloud Portal navigation, select **Administrator** -> **Tenants**.&#x20;
2. Select your **Tenant** name from the list.&#x20;
3. In the **Settings** tab, click **Add**. The **Add Tenant Feature** pane displays.&#x20;
4. From the **Select Feature** item list, select **Other**.&#x20;
5.  In the **Configuration** field, enter **block\_public\_network\_to\_azure\_storage**. \


    <div align="left">

    <figure><img src="../../.gitbook/assets/Screenshot (233).png" alt=""><figcaption><p>The <strong>Update Tenant Feature</strong> window filled to block public access to Azure <strong>Storage Accounts.</strong> </p></figcaption></figure>

    </div>
6. In the empty field, enter "**True**".&#x20;
7.  Click **Add**. Public access to storage accounts is blocked. \


    <div align="left">

    <figure><img src="../../.gitbook/assets/Screenshot (234).png" alt=""><figcaption><p>The <strong>Settings</strong> tab showing public access to <strong>Storage Accounts</strong> blocked.</p></figcaption></figure>

    </div>

###
