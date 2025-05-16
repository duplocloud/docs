---
description: Create Cloud Storage Buckets in GCP
---

# Cloud Storage

In GCP, Cloud Storage Buckets are containers that hold your data. Everything in Google Cloud Storage resides in a bucket. Learn more about [GCP Cloud Storage](https://cloud.google.com/storage/docs/introduction) and [Cloud Storage Buckets](https://cloud.google.com/storage/docs/buckets).

## Creating a GCP Cloud Storage Bucket

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Storage**. The **Buckets** page displays.

<div align="left"><figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.15-12_39_31 (1).png" alt=""><figcaption><p><strong>Buckets</strong> page in the DuploCloud Portal</p></figcaption></figure></div>

2. In the **Buckets** tab, click **Add**. The **Create a Bucket** pane displays.

<div align="left"><figure><img src="../../.gitbook/assets/my bucket image.png" alt="" width="563"><figcaption></figcaption></figure></div>

3. Configure the bucket settings:

* **Name**: Provide a unique name for the bucket.
* **Enable Versioning**: Optionally, enable this option to keep previous versions of uploaded files.
* **Allow Public Access**: Optionally, enable to allow public access.&#x20;
* **Labels**: Optionally, add labels to organize and categorize your bucket. For example:
  * Key: `env`, Value: `production`
* **Location Type**: Choose the location type for the bucket:
  * **Tenant Region**: Select this option to store the bucket in your specific Tenant region
  * **Multi-Region**: Store data across multiple regions for higher availability and redundancy.
  * **Region**: Store data in a specific geographic region, e.g., **US-Central1** (Iowa, USA).

4. Click **Create**. The bucket will be created based on the configurations you specified.
