---
description: Set up GCP billing data access for DuploCloud
---

# Enabling GCP Billing Data

To enable billing data visibility in DuploCloud for Google Cloud Platform (GCP), you must export detailed billing data to BigQuery and give DuploCloud access to that dataset. Once the export is complete, you will enable the billing feature in the DuploCloud Portal to begin viewing usage and cost data.

## Step 1. Create a BigQuery Dataset

[Create a BigQuery dataset](https://cloud.google.com/bigquery/docs/datasets#create-dataset) in the project you plan to use with DuploCloud.

## Step 2. Enable Billing Export to BigQuery

[Enable detailed billing data export](https://cloud.google.com/billing/docs/how-to/export-data-bigquery) using the following specifications:

* Select the same project and dataset you used in Step 1.
* Make sure to enable **Detailed usage** **cost** export.

## Step 3. Share the Dataset with DuploCloud

1. Open the BigQuery dataset in the GCP console.
2. Click **Share dataset**.
3. Add the DuploCloud service account email.
4. Assign the role: **BigQuery Data Viewer**.

## Step 4. Enable Billing in DuploCloud

After setting up the export and access:

1. In the DuploCloud Portal, navigate to **Administrator**-> **Billing**.
2.  On the right side of the page, click **Enable Billing Feature**.\


    <figure><img src="../../../.gitbook/assets/Screenshot (600) (2).png" alt=""><figcaption><p><strong>Billing</strong> page in the DuploCloud Portal with the <strong>Enable Billing Feature</strong> option highlighted</p></figcaption></figure>

DuploCloud will display GCP billing data as it becomes available from the BigQuery export.

## Step 5. Notify DuploCloud Support

Contact DuploCloud Support to confirm access and complete setup. This step is required to activate the billing dashboard.
