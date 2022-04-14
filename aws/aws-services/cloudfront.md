# CloudFront

## Create a CloudFront distribution

#### Prerequisite

S3 bucket needs to be created and static asserts need to be uploaded to the S3 bucket. Please follow the steps in the link below to create the S3 bucket.

{% content-ref url="s3-bucket.md" %}
[s3-bucket.md](s3-bucket.md)
{% endcontent-ref %}

Create Cloudfront distribution from **DevOps** > **App Integration** > **CloudFront** (tab)**+Add** button above the table.&#x20;

* Name - Friendly name for the distribution.
* Root Object - Default root object that will be returned while accessing the root of the domain. Example: index.html. Should not start with "/".
* Certificate - ACM certificate for the distribution. Only certs in us-east-1 can be used. If not already present should be created in AWS and added to the plan (Administrator > Plans > Select Tenant Plan > Certificate tab).
* Aliases - Domain name using which distribution will be accessed. Multiple domain names can be configured if needed. If the Domain name is managed by Duplo CNAME mapping will be automatically done else CNAME mapping should be added manually in the appropriate DNS management console.
* Origins - Location information where the actual content is stored. It can be an S3 bucket or any HTTP server endpoint.
  * Domain Name - S3 bucket can be selected or choose other and enter custom endpoint.
  * ID - unique identifier for the origin. UI pre-populates it from the domain name. If needed can be changed.
  * Path - Optional. The Path will be suffixed to the origin domain name (URL) while fetching content. For S3: If the content that needs to be served is under prefix static. You should enter "static" in the path. For custom url: If all the API have a prefix like v1. You should enter "v1" in the path.
* Default Cache Behaviors - Default Cache policy and the default origin to fetch content are entered here.
  * Cache Policy ID - AWS predefined cache policies are listed. You can select one or choose other and enter a custom cache policy.&#x20;
  * Target Origin - Choose the default origin that should be used for the distribution
* Custom Cache Behaviors - Additional Cache policies and path patterns to use the custom cache behaviors are entered here.
  * Cache Policy ID - AWS predefined cache policies are listed. You can select one or choose other and enter a custom cache policy.&#x20;
  * Path Pattern - For request matching the pattern enter this specific origin and cache policy will be used. Example "**api/\***" all requests that starts with api prefix will be routed to this origin.
  * Target Origin - Choose the origin that should be used for this custom path.

![](../../.gitbook/assets/cloudfrontdistribution-form.jpg)

{% hint style="info" %}
Note: If the S3 bucket used is part of the same tenant where cloudfront distribution is created. Duplo creates an Origin Access Identity and updates the bucket policy to allow GetObject for cloudfront Origin Access Identity. No extra step is needed on the user end to deal with S3 bucket permissions.
{% endhint %}

## Lambda Association

Create the lambda function in the tenant by selecting the `Edge lambda` checkbox. This will create a lambda function in `us-east-1` along with necessary permissions.

Create a CloudFront distribution by giving the necessary values, in addition for the lambda@edge select the function associations and select the lambda function.

{% hint style="info" %}
**Note:** We will show the versions of the lambda function, so same function will be there multiple times with V1 and V2.
{% endhint %}

Once the deployment status becomes `Deployed`. Then visit the domain name and you should see the invocation of the lambda function

## Maintenance Page setup for website

* Default origin should point to your app url `ui.mysite.com.`
* Create a new S3 Bucket to store maintenance pages. In the bucket create a prefix/folder called `maintpage.`
* Upload maintenance page asserts (html,css,js etc) into S3 bucket inside `maintpage` folder.
* Add new **S3 Origin** pointing to S3 bucket we have maintenance static asserts.
* Add new **Custom Cache Behaviors** use `/maintpage/*`as path pattern, Target origin should be S3  maintenance asserts origin.
* Adding **Custom Error Response** mapping**.**
  * &#x20;**** In **error code** dropdown select the HTTP code for which the maintenance page should be served. **502** gateway timeout is commonly used.
  * In **Response page path** enter `/maintpage/5xx.html`. 5xx.html should be changed to a page that exists in s3.
  * HTTP Response code can be either 200 or 502 (same as the actual source origin response code).
