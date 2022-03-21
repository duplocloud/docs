# Lambda

## Create a lambda function <a href="#0-toc-title" id="0-toc-title"></a>

Navigate to **DevOps > Serverless > Lambda tab > +Add** button. Give a name for the Lambda function and other values. This will create the lambda function. Click on **AWS console** to go to the console shell for this function. Test the function. You can look at the tutorial above for the same or look at the AWS documentation.

![](https://duplocloud.com/wp-content/uploads/2021/11/lambdamenu.png)

## Updating lambda function and configuration <a href="#1-toc-title" id="1-toc-title"></a>

To update the code for the Lambda function, create a new package with a different name and upload in S3 bucket again. Then select the lambda function in the table and click Edit under dropdown menu in Actions column. Make sure the right S3 bucket has been selected and provide the name of the function. To update a function configuration like timeout memory, etc. use the edit configuration button.

## Integrating with other resources <a href="#2-toc-title" id="2-toc-title"></a>

DuploCloud enables you to create a classic micro-services based architecture where your Lambda function can integrate with any other resource within your tenant like S3, Dynamo, RDS or other Docker based microservices. DuploCloud will implicitly enable the Lambda function to communicate with other resources but block any communication outside the tenant (except ELB).

## Trigger and event sources <a href="#3-toc-title" id="3-toc-title"></a>

To setup a trigger or event source, the resource needs to be created via the DuploCloud Portal. Subsequently, one could trigger directly from that resource to the Lambda function in the AWS console menu of your Lambda function. Resources could be S3 buckets, API Gateway, DynamoDB, SNS etc. An example trigger via API Gateway was described in the tutorial.

## Passing secrets <a href="#4-toc-title" id="4-toc-title"></a>

Passing secrets to a Lambda function can be done in much the same way as passing secrets to your Docker based service i.e., using environmental variables. For example, you can create a relational database from the **Database > RDS** menu in DuploCloud, provide username and password, then in the Lambda menu give the same username and password. No secrets need to be stored anywhere outside like vault, git repo, etc.
