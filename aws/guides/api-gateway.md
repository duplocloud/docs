# API gateway

AWS ApiGateway RestApi is created from the DuploCloud Portal which will take care of creating the security policies to make the API Gateway accessible to other resources (like Lambda function) within the tenant. From the DuploCloud Portal only create the RestApi. All other configuration for the API (like defining methods, resources and pointing to lambda functions) should be done in the AWS console. The console for the API can be reached by selecting the API in **DevOps > Networking > API Gateway** table and then clicking on the Console button under the Actions menu. The above tutorial displays the integration of API Gateway and lambda function.

![](https://duplocloud.com/wp-content/uploads/2021/11/apigateway.png)
