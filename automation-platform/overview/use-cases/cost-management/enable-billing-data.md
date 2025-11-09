---
description: Enable billing data in the DuploCloud Portal
---

# Enabling AWS Billing Data

## Prerequisites

To enable the billing feature in DuploCloud, ensure the following:

* **Enable billing data export in AWS:** Follow the steps in [this AWS guide](https://docs.aws.amazon.com/cur/latest/userguide/what-is-cur.html) to enable cost and usage reports.
* **Apply cost allocation tags:** These tags are required for DuploCloud to organize and retrieve billing data accurately. For more details, see the [DuploCloud cost allocation tags documentation](cost-allocation-tags.md).&#x20;
* **Access requirements:** You must be logged in as `root` (or an equivalent IAM user with full billing permissions) on the AWS account that manages cost and billing for your AWS organization.

## Enabling Billing Data in DuploCloud

1. In the DuploCloud Portal, go to **Administrator** -> **Billing**.
2.  On the right side of the page, click **Enable Billing Feature**. Billing data will display after the next data sync.\


    <figure><img src="../../../../.gitbook/assets/Screenshot (600) (1).png" alt=""><figcaption><p><strong>Billing</strong> page in the DuploCloud Portal with <strong>Enable Billing Feature</strong> option highlighted</p></figcaption></figure>
