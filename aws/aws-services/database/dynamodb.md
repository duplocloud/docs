# DynamoDB

Create DynamoDB from under **DevOps > Database > DynamoDb tab > +Add** button above the table.&#x20;

The required permissions to access the DynamoDB from VM, Lambda functions and containers are provisioned automatically through Instance profiles and hence no Access key is required in the Application code.

&#x20;Application code should use the IAM role/Instance profile approach to connect to these services i.e., the AWS SDK constructor which only uses region should be used.

&#x20;More detailed configuration of the DynamoDB can be done directly in the AWS console which can be accessed by clicking on the Console `>_` icon. Within this login the user will have enough permissions to configure the desired application specific details of the DynamoDB. But no access or security level permissions will be provided.

