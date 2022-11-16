# Create Lambda using Container Image

DuploCloud provides the ability to configure Lambda using Container Images.

## Step 1: Build Container Image <a href="#0-toc-title" id="0-toc-title"></a>

Create and Build your Lambda code using DockerFile.  Refer to the AWS documentation for detailed instructions on how to build and test Container Images.

## Step 2: Create ECR Repository <a href="#0-toc-title" id="0-toc-title"></a>

&#x20;Navigate to **DevOps** > **Storage** > **ECR Repository.** Give Name of the Repository\
![](<../../../.gitbook/assets/image (70).png>)

## Step 3: Upload Container Images to ECR Repository <a href="#0-toc-title" id="0-toc-title"></a>

As a first step, login to ECR. You would need to tag the built Images and push the Images to the ECR Repository created at Step2.&#x20;

Refer to the AWS Documentation on detail steps for uploading Container Images

## Step 4: Configure Lambda with Container Images

Navigate to **DevOps** > **Serverless** > **Lambda**\
Select Package Type as _Image._

Provide the Image URI&#x20;

![Lambda screen](<../../../.gitbook/assets/image (4) (3).png>)
