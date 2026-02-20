---
description: Configure CloudFront distributions in DuploCloud
---

# CloudFront Distributions

[CloudFront](https://aws.amazon.com/cloudfront/) is an AWS content delivery network (CDN) that accelerates delivery of your content by caching it at edge locations closer to your users.

## Prerequisites

Before creating a CloudFront distribution:

* [Create an S3 bucket](../../../../overview/aws-services/s3-bucket.md#creating-an-s3-bucket)
* Upload your static assets to the S3 bucket.

## Creating a CloudFront Distribution

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Networking**.
2. Select the **CloudFront** tab.
3. Click **Add**. The **Add Distribution** page displays.

<div align="left"><img src="../../../../.gitbook/assets/cloudfrontdistribution-form.jpg" alt=" CloudFront Add Distribution page."></div>

4. Complete the following fields:

<table data-header-hidden><thead><tr><th width="185.5555419921875"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the distribution.</td></tr><tr><td><strong>Root Object</strong></td><td>Specify the Root Object that will be returned when accessing the domain's root (e.g., <code>index.html</code>). The Root Object should not start with <code>/</code>.</td></tr><tr><td><strong>Certificate</strong></td><td>Select the ACM certificate for the distribution. Only certificates issued in <strong>US-East-1</strong> are valid. If no certificate is available, request one in AWS and add it to the DuploCloud Plan.</td></tr><tr><td><strong>Certificate Protocol Version</strong></td><td>Select the correct Certificate Protocol Version from the list.</td></tr><tr><td><strong>CORS Allowed Hosts</strong></td><td>Optionally, enter the list of origins allowed for cross-origin resource sharing (CORS).</td></tr><tr><td><strong>Logging</strong></td><td>Optionally, enable or disable logging for the CloudFront distribution.</td></tr><tr><td><strong>Aliases</strong></td><td>Optionally, enter any alternate domain name(s) (CNAMEs) to associate with the CloudFront distribution. For aliases managed by DuploCloud, CNAME mapping is automatic. For others, you must manually create the CNAME record in your DNS console.</td></tr><tr><td><strong>Origins</strong></td><td>Enter the location(s) where the content is stored:<br>• <strong>Domain Name</strong>: Select the correct S3 bucket, or choose Other and enter a custom origin endpoint.<br>• <strong>Origin ID</strong>: This unique ID is pre-populated from the domain name; you can change it if needed.<br>• <strong>Path</strong>: (Optional) Enter a path suffix to append to the origin's domain name when fetching content. Examples: <code>static</code> for S3 prefix, <code>v1</code> if all APIs start with <code>/v1</code>.</td></tr><tr><td><strong>Default Cache Behavior</strong></td><td>Configure how CloudFront caches and serves content by setting the following:<br>• <strong>Target Origin</strong>: Select the origin to fetch content from.<br>• <strong>Cache Policy ID</strong>: Select one of the AWS-defined cache policies or specify a custom one.<br>• <strong>Origin Request Policy</strong>: Define headers, cookies, and query strings to include in origin requests.<br>• <strong>Response Headers Policy</strong>: Set headers included in CloudFront responses.<br>• <strong>Compress</strong>: Optionally enable compression for better performance.</td></tr><tr><td><strong>Custom Cache Behaviors</strong></td><td>Optionally, configure additional cache behaviors with the following fields:<br>• <strong>Path Pattern</strong>: Enter the URL path pattern to match requests (e.g., <code>api/*</code>).<br>• <strong>Cache Policy ID</strong>: Select or enter the cache policy to apply.<br>• <strong>Target Origin</strong>: Choose the origin for these requests.<br>• <strong>Origin Request Policy ID</strong>: Specify which origin request policy to apply.<br>• <strong>Response Headers Policy</strong>: Define response headers for this behavior.<br>• <strong>Compress</strong>: Enable compression if desired.</td></tr><tr><td><strong>Cache Policy ID</strong></td><td>Select one of the AWS-defined cache policies, or choose <strong>Other</strong> to enter a custom policy ID.</td></tr><tr><td><strong>Function Associations</strong></td><td>Attach Lambda@Edge functions to CloudFront events by specifying:<br>• <strong>origin-request</strong> (<strong>Include Body</strong> option available)<br>• <strong>origin-response</strong><br>• <strong>viewer-request</strong> (<strong>Include Body</strong> option available)<br>• <strong>viewer-response</strong></td></tr><tr><td><strong>Custom Error Responses</strong></td><td>Configure custom error handling:<br>• <strong>HTTP Error Code</strong>: The HTTP status code to handle (e.g., <code>404</code>).<br>• <strong>Error Caching TTL</strong>: Time to cache the error response.<br>• <strong>Response Page Path</strong>: The path to the custom error page.<br>• <strong>HTTP Response Code</strong>: The HTTP response code CloudFront returns to the viewer.</td></tr></tbody></table>

5. Click **Submit** to create the CloudFront distribution.&#x20;

**For Terraform Users**: When deploying a CloudFront distribution using Terraform in DuploCloud, ensure that the `comment` field is included in your configuration. Although this field is marked optional in AWS documentation, DuploCloud requires it as a resource name. Omitting it may cause deployment failures.

## Creating a Lambda@Edge function association

### Creating a Lambda function in the Tenant

1. Select the Tenant from the **Tenant** list box.
2. Navigate to **Cloud Services** -> **Serverless**.
3. Select the **Lambda** tab.
4. Click **Add**.
5. Select the **Edge lambda** checkbox to create a Lambda function in **us-east-1** with the necessary permissions.
6. Complete the necessary fields and click **Submit**.

### Creating a CloudFront distribution

1. Select the **Tenant** from the **Tenant** list box.
2. Navigate to **Cloud Services** -> **Networking**, select the **CloudFront** tab, and click **Add**.
3. Complete the necessary fields. Make sure to select the Lambda function created above in Function **Associations**.
4. Click **Submit**.

{% hint style="info" %}
**Note:** DuploCloud lists **all versions** of the Lambda function (e.g., **v1**, **v2**, etc.). Select the correct version for your use case.
{% endhint %}

Once the deployment status is **Deployed**, visit the distribution’s domain name to verify Lambda function invocation.

## **Setting Up a Website Maintenance Page**

You can use CloudFront to serve a maintenance page during outages or deployments.

1. The default origin should point to your app (e.g., `ui.mysite.com`).
2. Create a new S3 bucket to store maintenance page assets.
3. In that bucket, create a folder (prefix) named `maintpage`.
4. Upload your maintenance page files (`index.html`, `style.css`, etc.) into the `maintpage` folder.
5. In CloudFront:
   * Add a **new S3 Origin** pointing to this S3 bucket.
   * Add a **Custom Cache Behavior**:
     * **Path Pattern:** `/maintpage/*`
     * **Target Origin:** the S3 origin created for maintenance assets

## **Adding Custom Error Response Mapping**

To serve the maintenance page during errors:

1. When creating a distribution, in **Custom Error Responses**, configure the following settings:

<table data-header-hidden><thead><tr><th width="228.22222900390625"></th><th></th></tr></thead><tbody><tr><td><strong>HTTP Error Code</strong></td><td>Specify the error code (e.g., <code>404</code>, <code>500</code>) that triggers the custom response.</td></tr><tr><td><strong>Error Caching TTL</strong></td><td>Specify the time (in seconds) to cache the error response.</td></tr><tr><td><strong>Response Page Path</strong></td><td>Enter the path to the custom error page (e.g., <code>/custom-404.html</code>).</td></tr><tr><td><strong>HTTP Response Code</strong></td><td>Specify the response code to return with the custom error page (e.g., <code>20</code>0 or <code>302</code>).</td></tr></tbody></table>
