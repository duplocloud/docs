# S3 bucket

Create S3 Bucket from **DevOps** > **Storage** > **S3** > **+Add** button above the table. Provide the name and select _S3Bucket_ from the dropdown. The required permissions to access the S3 bucket from VM, Lambda functions and containers is provisioned automatically through Instance profiles and hence no Access key is required in the Application code. Application code should use the IAM role/Instance profile approach to connect to these services i.e., the AWS SDK constructor which only uses region should be used. Uploading the file and changing the bucket permissions can be done directly in the AWS console which can be accessed by clicking on the `>_` icon. Within this login the user will have enough permissions to configure the bucket, but no access or security level permissions will be given.

![Create S3](https://duplocloud.com/wp-content/uploads/2021/11/N2-S3.png)

### Add custom prefix for S3 buckets

DuploCloud provides the capabillity to specify a custom prefix for S3.&#x20;

Refer To enable this option, Goto **Admin** > **System Settings >** Add App Config ****&#x20;

Select **Key** as  'Prefix all S3 Bucket Name' from the dropdown, and specify the prefix label.

{% hint style="warning" %}
Avoid specifying system reserved prefixes like `duploservices-`
{% endhint %}

<figure><img src="../../.gitbook/assets/image (8) (4) (1).png" alt=""><figcaption><p>coustom prefix for S3</p></figcaption></figure>

#### Enable Tag based Property in DuploCloud

To use this capability, ensure `ENABLEAWSRESOURCEMGMTUSINGTAGS` property is set as `True` in the DuploCloud System. Please contact DuploCloud Support Team for assistance.&#x20;
