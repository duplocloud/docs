---
description: Use GitHub Actions to deploy a Lambda Image or S3 bucket update
---

# Update a Lambda function

Instead of deploying your Lambda code in the same pipeline as your infrastructure, you can use CI/CD and GitHub Actions pipelines. With DuploCloud's GitHub Actions integration, you can build and deploy [Lambda functions](../../aws/aws-services/lambda/) in your AWS account by deploying a Lambda image or by a package uploaded to an S3 bucket.

{% hint style="info" %}
For general information about deploying serverless applications with GitHub Actions in AWS, reference this [blog](https://aws.amazon.com/blogs/compute/using-github-actions-to-deploy-serverless-applications/).
{% endhint %}

## Update a Lambda container image&#x20;

Use the following code as a template to update a Lambda container image with GitHub Actions. In this example, the Lambda container image in the `mytenant` Tenant is built and deployed.

```bash
name: Build and Deploy
on:
  # (Optional) Allows users to trigger the workflow manually from the GitHub UI
  workflow_dispatch:

  # Triggers the workflow on push to matching branches
  push:
    branches:
      - develop
env:
  duplo_host: https://mysystem.duplocloud.net   # DuploCloud URL
  duplo_token: "${{secrets.DUPLO_TOKEN }}"	# DuploCloud Token
  TENANT_NAME: mytenant				# DuploCloud Tenant name
  DUPLO_TENANT_ID: tenant_id			# DuploCloud Tenant Id where lambda is deployed
  LAMBDA_NAME: mylambda				# Name of the lambda

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  build:
  # YOU SHOULD ALREADY HAVE THIS FROM THE PREVIOUS DOCUMENTATION SECTION
  # ...
  # ...    
  deploy:
    runs-on: ubuntu-latest
    needs:
      - build
    steps:
	# Deploy the new image to Lambda  
      - name: Deploy Lambda
        run: |
            curl -Ssf -H 'Content-type: application/json' \
              -H "Authorization: Bearer $duplo_token" -XPOST \
              "${duplo_host}/subscriptions/$DUPLO_TENANT_ID/UpdateLambdaFunction" \
              -d "{
                'FunctionName': 'duploservices-$TENANT_NAME-$LAMBDA_NAME',
                'ImageUri': \"${{ needs.build.outputs.image }}\"
            }"
```

## Update Lambda based on package in Amazon S3

Use the following code as a template to deploy your Lambda functions to an S3 bucket with GitHub Actions. In this example, the Lambda container image in the `mytenant` Tenant is built, deployed, and updated using an S3 bucket that contains `helloworld.zip`

<pre class="language-bash"><code class="lang-bash">  name: Build and Deploy
  on:
    # (Optional) Allows users to trigger the workflow manually from the GitHub UI
    workflow_dispatch:
  
    # Triggers the workflow on push to matching branches
    push:
      branches:
        - develop
  env:
    duplo_host: https://mysystem.duplocloud.net  # DuploCloud URL
    duplo_token: "${{secrets.DUPLO_TOKEN }}"	 # DuploCloud Token
    TENANT_NAME: mytenant			 # DuploCloud Tenant name
    DUPLO_TENANT_ID: tenant_id			 # DuploCloud Tenant Id where lambda is deployed
    LAMBDA_NAME: mylambda			 # Name of the lambda
  
  # A workflow run is made up of one or more jobs that can run sequentially or in parallel
  jobs:
    build:
    # YOU SHOULD ALREADY HAVE THIS FROM THE PREVIOUS DOCUMENTATION SECTION
    # ...
    # ...    
    deploy:
      runs-on: ubuntu-latest
      needs:
        - build
  deploy:
    runs-on: ubuntu-latest
    needs:
      - build
    steps:
	# Deploy by updating S3 bucket 
      - name: Deploy Lambda
        run: |
            curl --location --request POST '${duplo_host}/subscriptions/$DUPLO_TENANT_ID/UpdateLambdaFunction' \
            --header 'Authorization: Bearer &#x3C;CHANGE_DUPLO_TOKEM>' \
            --header 'Content-Type: application/json' \
<strong>            --data-raw '{
</strong>                "FunctionName": "duploservices-test-helloworld-128329325849",
                "S3Bucket": "duploservices-test-cftest-128329325849",
                "S3Key": "helloworld.zip"
<strong>            }'
</strong></code></pre>
