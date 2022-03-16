# CloudFront

## Lambda Association

Create the lambda function in the tenant by selecting the `Edge lambda` checkbox. This will create a lambda function in `us-east-1` along with necessary permissions.&#x20;

{% content-ref url="lambda.md" %}
[lambda.md](lambda.md)
{% endcontent-ref %}

![](<../../.gitbook/assets/create-lambda-functions.png>)

Create a CloudFront distribution by giving the necessary values, in addition for the lambda@edge select the function associations and select the lambda function.

![](<../../.gitbook/assets/serverless-lamda-setup.png>)

{% hint style="info" %}
**Note:** We will show the versions of the lambda function, so same function will be there multiple times with V1 and V2.
{% endhint %}

Once the deployment status becomes `Deployed`. Then visit the domain name and you should see the invocation of the lambda function

![](<../../.gitbook/assets/lambda-functions-deployement-preview.png>)
