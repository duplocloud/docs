---
description: Deploy a DuploCloud management portal with Amazon Web Services
---

# Deploy a DuploCloud Portal in AWS

Use this procedure to create an initial DuploCloud Portal deployment using AWS.

Step 1: [Create a CloudFormation stack](deploy-a-duplocloud-portal-in-aws.md#create-a-cloudformation-stack)

Step 2: [Set up DNS entries](deploy-a-duplocloud-portal-in-aws.md#set-up-dns-entries)

Step 3: [Enable Single Sign-On (SSO)](deploy-a-duplocloud-portal-in-aws.md#enable-single-sign-on-sso)

Step 4: [Confirm Access to DuploCloud Portal](deploy-a-duplocloud-portal-in-aws.md#confirm-access-to-duplocloud-portal)

## Prerequisites

Before you begin to create your deployment:

* [Create a new AWS account](https://aws.amazon.com/free/?trk=578b2801-ffbb-4021-a1db-01a0bafb3a4a\&sc\_channel=ps\&ef\_id=CjwKCAjwge2iBhBBEiwAfXDBR3ABxb9HejfSaFdz\_73vBm44YFAfr8qbxf6S0lXEU4YV-FRCNyZ1RBoCT4AQAvD\_BwE:G:s\&s\_kwcid=AL!4422!3!507162072479!p!!g!!aws!12563449882!121199905124\&all-free-tier.sort-by=item.additionalFields.SortRank\&all-free-tier.sort-order=asc\&awsf.Free%20Tier%20Types=\*all\&awsf.Free%20Tier%20Categories=\*all).
* Obtain [Administrator access](https://docs.aws.amazon.com/streams/latest/dev/setting-up.html) to the new AWS account
* Log in to the AWS account as an Administrator, selecting a [region ](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html)in which to host your deployment.

## Create a CloudFormation stack

You use CloudFormation to create an initial deployment.

1. Navigate to **Services** and select **CloudFormation**.
2. Select **Create stack - with new `resources (standard)`**.
3. In the **Prerequisite - Prepare template** section, select **Template is ready**.
4. In the **Specify template** section, select **Amazon S3 URL** as the template source.
5. Copy and paste [https://duplo-setup-resources.s3-us-west-2.amazonaws.com/duplo-root-stack.json](https://duplo-setup-resources.s3-us-west-2.amazonaws.com/duplo-root-stack.json) into the **Amazon S3 URL** field.&#x20;
6. Click **Create**.

After creating the stack, an EC2 instance is initiated in the AWS account using the associated AMI. The following table lists available AMIs based on the region that you target for the deployment:

<table><thead><tr><th width="347">Region</th><th>AMI ID Value</th></tr></thead><tbody><tr><td>ap-northeast-1</td><td>ami-0191c10b498d55752</td></tr><tr><td>ap-south-1</td><td>ami-0a41b5b9007e7f4cb</td></tr><tr><td>ca-central-1</td><td>ami-06e07d062e55ce3ca</td></tr><tr><td>eu-west-2</td><td>ami-0a568fd865d942af7</td></tr><tr><td>us-east-1</td><td>ami-019850d7e75ef6461</td></tr><tr><td>us-east-2</td><td>ami-00a7dd0e0dbecb276</td></tr><tr><td>us-west-1</td><td>ami-0bbbdc1ed9dbe79e3</td></tr><tr><td>us-west-2</td><td>ami-00af8b024a7f2935e</td></tr></tbody></table>

### Specify CloudFormation stack parameters

In the **Specify Stack Details** screen, set the following stack parameters:

* **Stack Name**: `duplo-root-stack`
* **MasterAmiId:** Select a value from the table in [Step 2](deploy-a-duplocloud-portal-in-aws.md#2.-create-a-cloudformation-stack), based on your region.
* **`ENABLEBASTION`:** **NO**
* **`SetupUrl`**: The URL you plan to use for your environment.  For example: `https://[`_`ENVIRONMANT-NAME`_`].mydomain.com`
* **`DUPLODNSPRFX`**: Use the format `${`_`ENVIRONMANT-NAME`_`}-apps.mydomain.com`
* **`DefaultAdmin`**: Your email address, as the first Administrative User.
* **`ENABLEJITAWSADMINAPI`**: `true`

When you have specified all stack parameters, click **Next** to specify stack failure options.

### Specify stack failure options

In the **Stack Failure Options** screen, set stack failure options.&#x20;

1. Select **Preserve successfully provisioned resources.**
2. Click **Next**.

You are ready to create the stack.

### Create the stack

After you have specified all parameters and options, create the stack.

1. In the **Review** page, verify the settings you entered for stack creation.
2. In the **Capabilities** dialog, select both Acknowledgments checkboxes.&#x20;
3. Click **Next** to execute and create the stack.&#x20;

Creating the stack takes between 10 to 15 minutes. Your CloudFormation Stack output is generated. You will need values from this output to create your deployment.

#### OpenVPN Subscription (optional)

While the stack is launching, take time to [subscribe to the OpenVPN Access Server AWS Marketplace offering](https://aws.amazon.com/marketplace/server/procurement?productId=fe8020db-5343-4c43-9e65-5ed4a825c931) to be aware of all important news and communications.&#x20;

## Set up DNS entries

To set up DNS entries for your DuploCloud deployment, you must collect these values from the generated CloudFormation Stack output.&#x20;

* `AuthELBDNS`
* `AppDnsNameServers`

Navigate to your DNS provider account where _\[`MY-DOMAIN].com`_ is managed and do the following.

1. Add a `CNAME` record for **Name**, using the value of**`SetupUrl`**, which you [previously specified](deploy-a-duplocloud-portal-in-aws.md#specify-cloudformation-stack-parameters).&#x20;
2. Add a `CNAME` record for **Value**, using the value of `AuthELBDNS`, which you [previously collected from the generated CloudFormation Stack output](deploy-a-duplocloud-portal-in-aws.md#create-the-stack).
3. Add an `NS` record for **Name**, using the value of **`DUPLODNSPRFX`**, which you [previously specified](deploy-a-duplocloud-portal-in-aws.md#specify-cloudformation-stack-parameters).
4. Add an `NS` record for **Value**, using the value of the nameservers collected by `AppDnsNameServers` from the [generated CloudFormation Stack output](deploy-a-duplocloud-portal-in-aws.md#create-the-stack).
5. Use [https://mxtoolbox.com/DnsLookup.aspx](https://mxtoolbox.com/DnsLookup.aspx) to validate these records.

## Enable Single Sign On (SSO)

Contact DuploCloud Support to enable Single Sign-On (SSO) for your deployment using Google SSO or Microsoft Account Login.

## Confirm Access to DuploCloud Portal

Navigate to the DuploCloud Portal URL in your browser and confirm you can authenticate. If you have problems, contact DuploCloud Support.
