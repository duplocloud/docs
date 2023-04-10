---
description: Create an S3 bucket for AWS storage
---

# S3 bucket

Amazon Simple Storage Service (Amazon S3) is an object storage service offering scalability, data availability, security, and performance. You can store and protect any data for data lakes, cloud-native applications, and mobile apps. Read more about S3 and its capabilities [here](https://aws.amazon.com/s3/).

## Creating an S3 bucket

1. In the DuploCloud Portal, navigate to **DevOps** -> **Storage**.
2. Click the **S3** tab.
3.  Click **Add**. The **Create an S3 Bucket pane displays**.

    ![Create S3](../../.gitbook/assets/AWS\_GCP\_Bucket\_add.png)
4. In the **Name** field, enter a name for the S3 bucket.
5. In the **Region** list box, select the region. You can select **Tenant Region**, **Default Region**, or **Global Region**, and specify **Other Region** to enter a custom region you have defined.

## Setting S3 bucket permissions

You can set specific bucket permissions using the DuploCloud Portal. Permissions for virtual machines, Lambda functions, and containers are provisioned automatically through Instance profiles, so no access key is required in your application code. However, when coding your application, be aware of these guidelines:

* Use the IAM role or Instance profile to connect to services.
* Only use the AWS SDK constructor for the region.

Set S3 Bucket permissions in the DuploCloud Portal:

1. In the DuploCloud Portal, navigate to **DevOps** -> **Storage**.
2. Click the **S3** tab.
3. From the **Name** column, select the bucket for which you want to set permissions. The **S3 Bucket** page for your bucket displays.
4. In the **Settings** tab, click **Edit**. The **Edit a S3 Bucket** pane displays.
5. From the **KMS** list box, select the key management system scope (**AWS Default KMS Key**, **Tenant KMS Key**, etc.).
6. Select only one of the following options: **Allow Public Access**, **Enable Access Logs**, **Enable Versioning**, or **Require SSL / HTTPS**.
7. Click **Save**. In the Details tab, your changed permissions are displayed.

Use this table to map the permission options above with the YAML key/value pair.&#x20;

| Edit a S3 Bucket Option | Key                         | Value  |
| ----------------------- | --------------------------- | ------ |
| **Allow Public Access** | `duplo-allow-public-access` | `true` |
| **Enable Access Logs**  | `duplo-enable-access-logs`  | `true` |
| **Enable Versioning**   | `enable-versioning`         | `true` |
| **Require SSL / HTTPS** | `duplo-policy`              | `ssl`  |

{% hint style="info" %}
From the **S3 Bucket** page, you can set bucket permissions directly in the AWS Console by clicking the **>\_Console** icon. You have permission to configure the bucket within the AWS Console session, but no access or security-level permissions are available.
{% endhint %}

### Granting public access to S3 buckets

To enable public access to S3 buckets, set the following key/value pairs:

<pre><code>duplo-policy  = publicread
<strong>duplo-allow-public-access  = True
</strong></code></pre>

### Add a custom prefix for S3 buckets

DuploCloud provides the capability to specify a custom prefix for S3.&#x20;

1. In the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Click the **System Config** tab.
3. Click **Add**. The **Add Config** pane displays.
4. From the **Config Type** list box, select **AppConfig**.
5. From the **Key** list box, select **Prefix all S3 Bucket Name**.
6. In the **Value** field, enter the custom prefix.
7. Click **Submit**.

{% hint style="warning" %}
Avoid specifying system-reserved prefixes such as`duploservices`.
{% endhint %}

<figure><img src="../../.gitbook/assets/AWS_GCP_Bucket_prefix.png" alt=""><figcaption><p><strong>Add Config</strong> pane for <strong>Key Prefix all S3 Bucket Name</strong></p></figcaption></figure>

### Enable tag-based properties in the DuploCloud Portal

To use this capability, ensure that the `ENABLEAWSRESOURCEMGMTUSINGTAGS` property is set to`True` in the DuploCloud System. Please get in touch with DuploCloud Support Team for assistance with this feature.
