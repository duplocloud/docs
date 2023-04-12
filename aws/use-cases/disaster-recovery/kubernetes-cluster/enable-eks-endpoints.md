---
description: Specify EKS endpoints for an Infrastructure
---

# Enable EKS endpoints

AWS SDKs and the AWS Command Line Interface (AWS CLI) automatically use the default public endpoint for each service in an AWS Region. However, you can specify alternate endpoints.

For more information about AWS Endpoints, see the [AWS documentation](https://docs.aws.amazon.com/general/latest/gr/rande.html).

## Specifying alternate EKS endpoints

1. Follow the steps in the section [Creating an Infrastructure](../../disaster-recovery.md). But before clicking **Create**, select **Advanced Options.**
2. Using the **Private Subnet CIDR** and **Public Subnet CIDR** fields, specify CIDRs for alternate public and private endpoints.&#x20;

{% hint style="info" %}
You can specify a **Private** endpoint, a **Public** endpoint, or both. If none are specified the default **Public** endpoint is used.
{% endhint %}
