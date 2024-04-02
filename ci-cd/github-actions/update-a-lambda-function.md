---
description: Use GitHub Actions to deploy a Lambda Image or S3 bucket update
---

# Update a Lambda function

Instead of deploying your Lambda code in the same pipeline as your infrastructure, you can use CI/CD and GitHub Actions pipelines. With DuploCloud's GitHub Actions integration, you can build and deploy [Lambda functions](../../aws/aws-services/lambda/) in your AWS account by deploying a Lambda image or by a package uploaded to an S3 bucket.

{% hint style="info" %}
For general information about deploying serverless applications with GitHub Actions in AWS, reference this [blog](https://aws.amazon.com/blogs/compute/using-github-actions-to-deploy-serverless-applications/).
{% endhint %}

### Update a Function Using an Image&#x20;

Use the following code as a template to update a Lambda container image with GitHub Actions. In this example, the Lambda container image in the `dev01` Tenant is updated and redeployed.

You must ensure the following are configured in your environment and your specific situation.&#x20;

* The name of lambda is set on the action to your actual lambda
* Duplocloud context configured correctly

<pre class="language-yaml"><code class="lang-yaml">name: Update Lambda

on: 
  workflow_dispatch:
    inputs:
      environment:
        description: The environment to deploy to
        type: environment
        default: dev01
      image:
        description: The full image
        type: string
        required: true

jobs:
  update_service:
    name: Update Lambda
    runs-on: ubuntu-latest
    environment: 
      name: ${{ inputs.environment }}
    env:
      DUPLO_TOKEN: ${{ secrets.DUPLO_TOKEN }}
      DUPLO_HOST: ${{ vars.DUPLO_HOST  }}
      DUPLO_TENANT: ${{ inputs.environment }}
    steps: 
    
    # configures duplocloud and aws
    - name: Cloud CI Setup
      uses: <a data-footnote-ref href="#user-content-fn-1">duplocloud/actions/setup@v0.0.3</a>

    # uses duploctl from above
    - name: Update Lambda
      uses: <a data-footnote-ref href="#user-content-fn-2">duplocloud/actions/update-image@v0.0.3</a>
      with:
        type: lambda
        name: mylambda
        image: ${{ inputs.image }}
</code></pre>

## Update Lambda based on package in Amazon S3

Use the following code as a template to deploy your Lambda functions to an S3 bucket with GitHub Actions. In this example, the Lambda in the `dev01` Tenant is updated using an S3 bucket that contains `mylambda-v1.zip`

You must ensure the following are configured in your environment and your specific situation.&#x20;

* Duplocloud context configured correctly
* `S3KEY`
* `S3BUCKET`
* `LAMBDA_NAME`

```yaml
name: Update Lambda

on: 
  workflow_dispatch:
    inputs:
      environment:
        description: The environment to deploy to
        type: environment
        default: dev01
      s3key:
        description: The key name in the s3 bucket with the version to deploy.
        type: string
        required: false
        default: mylambda-v1.zip

jobs:
  update_service:
    name: Update Lambda
    runs-on: ubuntu-latest
    environment: 
      name: ${{ inputs.environment }}
    env:
      DUPLO_TOKEN: ${{ secrets.DUPLO_TOKEN }}
      DUPLO_HOST: ${{ vars.DUPLO_HOST  }}
      DUPLO_TENANT: ${{ inputs.environment }}
    steps: 
    
    # configures duplocloud and aws
    - name: Cloud CI Setup
      uses: duplocloud/actions/setup@v0.0.3
      
    # we can build the bucket name using context from setup
    - name: Discover True Bucket Name
      env:
        S3BUCKET: mybucket
      run: echo "S3BUCKET=duploservices-${DUPLO_TENANT}-${S3BUCKET}-${AWS_ACCOUNT_ID}" >> $GITHUB_ENV

    # uses duploctl from above to run update lambda function
    - name: Update Lambda from S3
      env:
        LAMBDA_NAME: mylambda
        S3KEY: ${{ inputs.s3key }}
      run: duploctl lambda update_s3 $LAMBDA_NAME $S3BUCKET $S3KEY
```

### References

* [Duploctl Lambda Resource](https://github.com/duplocloud/duploctl/wiki/Lambda)
* [AWS Working with Lambda container images](https://docs.aws.amazon.com/lambda/latest/dg/images-create.html)
* Dockerhub Lambda Base Images
  * [Python](https://hub.docker.com/r/amazon/aws-lambda-python)
  * [NodeJS](https://hub.docker.com/r/amazon/aws-lambda-nodejs)
  * [GoLang](https://hub.docker.com/r/amazon/aws-lambda-go)
  * [Ruby](https://hub.docker.com/r/amazon/aws-lambda-ruby)
* [AWS Deploying Lambda functions as .zip file archives](https://docs.aws.amazon.com/lambda/latest/dg/configuration-function-zip.html)

[^1]: [https://github.com/duplocloud/actions/tree/main/setup](https://github.com/duplocloud/actions/tree/main/setup)

[^2]: [https://github.com/duplocloud/actions/tree/main/update-image](https://github.com/duplocloud/actions/tree/main/update-image)
