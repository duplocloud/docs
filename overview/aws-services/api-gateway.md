# API gateway

AWS ApiGateway RestApi is created from the DuploCloud Portal which will take care of creating the security policies to make the API Gateway accessible to other resources (like Lambda function) within the tenant. From the DuploCloud Portal only create the RestApi. All other configuration for the API (like defining methods, resources and pointing to lambda functions) should be done in the AWS console. The console for the API can be reached by navigating to **Cloud Services** -> **Networking**, selecting the **API Gateway** tab and then clicking on the **Console** button under the Actions menu. The above tutorial displays the integration of API Gateway and lambda function.

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.19-16_27_56.png" alt=""><figcaption></figcaption></figure>
