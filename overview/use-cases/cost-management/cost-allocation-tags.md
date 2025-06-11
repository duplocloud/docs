---
description: Activating cost allocation tags in DuploCloud AWS
---

# Apply cost allocation tags

The **duplo-project** cost allocation tag must be activated after you enable IAM access to billing data. Use the same AWS user and account that you used to enable IAM access to activate cost allocation tags.

It may take 1-2 days for new cost allocation tags to propagate in AWS. After that, DuploCloud's billing features will be fully functional and you can use the tag as a filter in the AWS Billing Cost Explorer.

Cost allocation tags can only be used to filter cost data generated after they are added.

To apply and activate cost allocation tags, follow the steps in [this document](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/activating-tags.html).

After you activate the tag successfully, you should see this screen:&#x20;

![Successful activation of cost allocation tags.](../../../.gitbook/assets/cost-tags.png)
