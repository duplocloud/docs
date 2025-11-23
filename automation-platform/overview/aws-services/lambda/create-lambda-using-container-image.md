---
description: Using Container Images to configure Lambda
---

# Configure Lambda with Container Images

Lambda container images allow you to package and deploy Lambda functions as Docker container images. By using container images, you can include custom libraries, runtimes, and dependencies that are not available in the standard Lambda execution environment. The process involves building the container image, storing it in Amazon Elastic Container Registry (ECR), and configuring Lambda to use the image for function execution.

## Building Container Images <a href="#id-0-toc-title" id="id-0-toc-title"></a>

Create and Build your Lambda code using `DockerFile`.  Refer to the [AWS documentation](https://docs.aws.amazon.com/lambda/latest/dg/configuration-function-zip.html) for detailed instructions on how to build and test container Images.

## Using Amazon ECR with Lambda

To use container images with Lambda, your images must be stored in Amazon Elastic Container Registry (ECR). ECR provides a fully managed service to store your container images, which Lambda pulls to run your functions.

For detailed instructions on how to configure and use ECR with Lambda, refer to the [DuploCloud ECR documentation](../elastic-container-registry-ecr/).

## Configuring Lambda with Container Images

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Serverless**.
2. Click the **Lambda** tab. The **Lambda Function** page displays.
3.  Click **Add**. The **Create a Lambda Function** page displays.<br>

    <figure><img src="../../../../.gitbook/assets/Screenshot (62).png" alt=""><figcaption><p><strong>Create a Lambda Function</strong> page <br></p></figcaption></figure>
4. In the **Name** field, enter the name of your Lambda Function.
5. In the **Description** field, enter a useful description of the function.
6. From the **Package Type** list box, select **Image**. For type **Zip**, see the [Lambda Functions](./) topic.
7. Configure the remaining fields as needed for your specific function.
8. If needed, [test the Lambda function](./#testing-a-lambda-function) to ensure it works properly.

## References

* [AWS Working with Lambda container images](https://docs.aws.amazon.com/lambda/latest/dg/images-create.html)
* Dockerhub Lambda Base Images:
  * [Python](https://hub.docker.com/r/amazon/aws-lambda-python)
  * [NodeJS](https://hub.docker.com/r/amazon/aws-lambda-nodejs)
  * [GoLang](https://hub.docker.com/r/amazon/aws-lambda-go)
  * [Ruby](https://hub.docker.com/r/amazon/aws-lambda-ruby)
