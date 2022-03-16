# S3 bucket

Create S3 Bucket from **DevOps** > **Storage** > **S3** > **+Add** button above the table. Provide the name and select _S3Bucket_ from the dropdown. The required permissions to access the S3 bucket from VM, Lambda functions and containers is provisioned automatically through Instance profiles and hence no Access key is required in the Application code. Application code should use the IAM role/Instance profile approach to connect to these services i.e., the AWS SDK constructor which only uses region should be used. Uploading the file and changing the bucket permissions can be done directly in the AWS console which can be accessed by clicking on the `>_` icon. Within this login the user will have enough permissions to configure the bucket, but no access or security level permissions will be given.

![](https://duplocloud.com/wp-content/uploads/2021/11/N2-S3.png)
