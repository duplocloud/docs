---
description: Activating cost allocation tags in DuploCloud AWS
---

# Apply cost allocation tags

DuploCloud requires the `duplo-project` cost allocation tag to be activated in your AWS account to enable full billing visibility and filtering features. Once activated, this tag can be used in tools like the **AWS Billing Cost Explorer** to filter and analyze costs associated with your DuploCloud projects.

## Prerequisites

Before activating cost allocation tags, ensure that:

* [IAM access to billing data](enable-billing-data.md) has been enabled for the AWS user you plan to use.
* You are using the **same AWS account and user** that was configured for billing access in DuploCloud.

## Activating Cost Allocation Tags

1. Log in to the [AWS Billing and Cost Management console](https://console.aws.amazon.com/billing/home#/).
2. Navigate to **Cost Allocation Tags**.
3. Locate the `duplo-project` tag in the list.
4. Select the checkbox next to it and click **Activate**. The `duplo-project` tag will begin filtering cost data going forward. Past cost data generated before the tag was added will not be affected.

{% hint style="info" %}
&#x20;It may take up to 24 to 48 hours for new cost allocation tags to propagate in AWS. After that, DuploCloud's billing features will be fully functional and you can use the tag as a filter in the AWS Billing Cost Explorer.
{% endhint %}

## Verifying Tag Activation

After successful activation, you should see the tag listed under **Active Tags** in the AWS Billing console, as seen in the image below. The DuploCloud Platform will begin reflecting cost data grouped by project as the data becomes available.

![Successful activation of cost allocation tags.](../../../.gitbook/assets/cost-tags.png)
