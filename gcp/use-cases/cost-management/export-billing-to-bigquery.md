# Export Billing to BigQuery

This guide provides step-by-step instructions for exporting your Google Cloud Platform (GCP) billing data to BigQuery. By doing so, you can leverage DuploCloud's dashboard to monitor and analyze your GCP billing effectively.&#x20;

## Pre-requisits

* A Google Cloud Platform account with billing enabled.
* Permissions to access the Google Cloud Billing API and BigQuery.

```
#Following permissions are needed to enable the billing
1. Billing Account Administrator
2. BigQuery Admin
```

* DuploCloud portal for monitoring the billing data.

## Step 1 : Create BigQuery Dataset

1. Navigate to the BigQuery Console in your Google Cloud Platform account.
2. Choose the project where you want to create the dataset from the drop-down list at the top of the page.
3.  Click on the "Create Dataset" button.\


    <figure><img src="../../../.gitbook/assets/image.png" alt="" width="563"><figcaption><p>Select Create Dataset</p></figcaption></figure>
4.  Configure your dataset:

    * **Dataset ID**: Enter a unique name for your dataset.
    * **Location Type**: Choose the `Multi-region`
    * **Default table expiration**: Set a default expiration time for tables in this dataset for 60 days. Tables will be automatically deleted after this period.
    * Click on the "Create dataset" button to finalize the creation.
    * Once the dataset is created, it should appear in the BigQuery Console under your project. You can click on the dataset to view its details.\


    <figure><img src="../../../.gitbook/assets/image (2).png" alt="" width="375"><figcaption><p>Fill in appropriate values to create dataset</p></figcaption></figure>



## Step 2 : Enable billing export to BigQuery

1. Go to the Google Cloud Console.
2. Select the "Billing" option from the main menu or visit Google Cloud Billing.
3. Select the billing account for which you want to enable the billing export.
4. In the billing account details page, select `Billing export` from the left-hand menu.
5.  Click on `Edit settings` under the `Detailed usage cost` section.\


    <figure><img src="../../../.gitbook/assets/image (135).png" alt="" width="563"><figcaption><p>Edit "Detailed usage cost" under the Billing export</p></figcaption></figure>
6.  Configure `Edit Detailed usage cost`

    * **Select the Project**: Choose the project where you created the BigQuery dataset.
    * **Select the Dataset**: Choose the dataset you created for billing data.
    * **Click "Save"**: Once you have selected the project and dataset.\


    <figure><img src="../../../.gitbook/assets/image (136).png" alt="" width="563"><figcaption><p>Put appropriate details and save the form</p></figcaption></figure>

Note: The exported billing data will include detailed information about your GCP usage and charges. Make sure to regularly monitor and analyze this data to keep track of your cloud spending.

Once the above steps are complete, please reach out to DuploCloud support team to complete some additional steps to enable the billing dashboard.

\
