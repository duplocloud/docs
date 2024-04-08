---
description: Create an Certificate for AWS Certificate Manager
---

# ACM Certificate

The DuploCloud platform needs a wild character AWS Certificate Manager (ACM) certificate that corresponds to the domain you created for the [Route 53 Hosted Zone](route-53-hosted-zone.md).&#x20;

For example, if the Route 53 Hosted Zone created is `apps.acme.com`, then the ACM certificate specifies `*.apps.acme.com`. You can add additional domains to this certificate (for example,  `*.acme.com`.

The ACM certificate is used with AWS Elastic Load Balancers (ELBs) that are created as part of DuploCloud application deployment. Follow this [AWS guide to issue an ACM certificate](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html#request-public-console).&#x20;

Once the certificate is issued, add the Amazon Resource Name (ARN) of the certificate in the DuploCloud Plan so that it is available to subsequent configurations, starting with the DuploCloud **default** plan.&#x20;

## Adding an ACM Certificate with ARN to a DuploCloud Plan

1. In the DuploCloud Platform, navigate to **Administrator** -> **Plans**. The **Plans** page displays.
2. Select the **DEFAULT** Plan from the **Name** column.
3. Click the **Certificates** tab.
4. Click **Add**.
5. In the **Name** field, enter a certificate name.
6. In the **Certificate ARN** field, enter the ARN.
7. Click Create. The ACM Certificate with ARN is created.

{% hint style="info" %}
Note that the ARN Certificate must be set for every new Plan created in a DuploCloud Infrastructure.
{% endhint %}
