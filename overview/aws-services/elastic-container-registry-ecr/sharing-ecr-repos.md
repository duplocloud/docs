# Sharing ECR Repos

You can grant another AWS account access to the images stored in your Amazon Elastic Container Registry (ECR) by configuring a repository policy. This allows external AWS accounts to pull (download) or push (upload) container images to your repository. Granting such access is useful when you need to share container images with other teams, partners, or automated systems that require access to your ECR repository.

There are different requirements for EKS/ECS and Lambda.

## Granting EKS and ECS Access to Your ECR Repository

To grant access to your ECR repository, [create a repository policy](https://docs.aws.amazon.com/AmazonECR/latest/userguide/set-repository-policy.html) using one of the policies below. Replace `ACCOUNT_ID` with the ID of the AWS account that needs access to the repository (not the account that contains the repo you are sharing).

### Allowing Pull (Read) Access

This policy allows the other AWS account to pull (download) images from your ECS repository.&#x20;

```
{
  "Version": "2008-10-17",
  "Statement": [
    {
      "Sid": "AllowPull",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::ACCOUNT_ID:root"
      },
      "Action": [
        "ecr:GetDownloadUrlForLayer",
        "ecr:BatchGetImage",
        "ecr:BatchCheckLayerAvailability"
      ]
    }
  ]
}
```

### Allowing Pull and Push (Read and Write) Access

This policy allows the other AWS account to pull (download) and push (upload) images from your ECS repository.&#x20;

```
{
  "Version": "2008-10-17",
  "Statement": [
    {
      "Sid": "AllowPullAndPush",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::ACCOUNT_ID:root"
      },
      "Action": [
        "ecr:GetDownloadUrlForLayer",
        "ecr:BatchGetImage",
        "ecr:BatchCheckLayerAvailability",
        "ecr:PutImage",
        "ecr:InitiateLayerUpload",
        "ecr:UploadLayerPart",
        "ecr:CompleteLayerUpload"
      ]
    }
  ]
}
```

## Granting Lambda Access

To use the repository for Lambda function images, you also need to [grant permissions directly to the Lambda service](https://docs.aws.amazon.com/lambda/latest/dg/images-create.html#gettingstarted-images-permissions). For example, here is the "read" policy from above with an `AllowLambdaPull` statement added that grants them. Replace `ACCOUNT_ID`  and `REGION_NAME` with the ID and region of the AWS account that needs access to the repository (not the account that contains the repo you are sharing).

```
{
  "Version": "2008-10-17",
  "Statement": [
    {
      "Sid": "AllowPull",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::ACCOUNT_ID:root"
      },
      "Action": [
        "ecr:GetDownloadUrlForLayer",
        "ecr:BatchGetImage",
        "ecr:BatchCheckLayerAvailability"
      ]
    },
    {
      "Sid": "AllowLambdaPull",
      "Effect": "Allow",
      "Action": [
        "ecr:BatchGetImage",
        "ecr:GetDownloadUrlForLayer"
      ],
      "Principal": {
        "Service": "lambda.amazonaws.com"
      },
      "Condition": {
        "StringLike": {
          "aws:sourceARN": "arn:aws:lambda:REGION_NAME:ACCOUNT_ID:function:*"
        }
      }
    }
  ]
}
```
