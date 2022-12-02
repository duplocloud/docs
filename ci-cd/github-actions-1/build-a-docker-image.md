---
description: Use Duplo to build and push a docker image from Gitlab CI/CD
---

# Build a docker image

## Case: Build and Push to DockerHub

The goal of this section is to show how you can build a docker image and push it to DockerHub.

It does three basic things:

* Logs in to DockerHub
* Builds and tags your docker image, with the tag based on the git commit SHA.
* Pushes your docker image

### Example Workflow

Here is an example gitlab workflow that builds a docker image and pushes it to DockerHub.

To use it you will need to change:

* `DOCKERHUB_USERNAME`variable
* `DOCKERHUB_REPO`variable
* `DUPLO_HOST`variable
* `DUPLO_SERVICE_NAME`variable
* `TENANT_NAME`variable

```yaml
variables:
  DOCKERHUB_USERNAME: duplocloud               # CHANGE ME!
  DOCKERHUB_REPO: mydockerhubid/myrepo         # CHANGE ME!
  DUPLO_HOST: https://mysystem.duplocloud.net  # CHANGE ME!
  DUPLO_SERVICE_NAME: myservice                # CHANGE ME!
  TENANT_NAME: mytenant                        # CHANGE ME!

docker-build:
  # Use the official docker image.
  image: docker:latest
  stage: build
  services:
    - docker:dind
  before_script:
    - docker login -u "$DOCKERHUB_USERNAME" -p "$DOCKERHUB_PASSWORD"
  script:
    - |
      tag=":$CI_COMMIT_SHA"
      echo "Running on branch '$CI_COMMIT_BRANCH': tag = $tag"
    - docker build --pull -t "$DOCKERHUB_REPO${tag}" .
    - docker push "$DOCKERHUB_REPO${tag}"
  # Run this job in a branch where a Dockerfile exists
  rules:
    - if: $CI_COMMIT_BRANCH
      exists:
        - Dockerfile
```

## Case: Build and Push to Amazon ECR (Elastic Container Reggistry)

The goal of this section is to show how you can build a docker image and push it to Amazon ECR.

It does three basic things:

* Logs in to Amazon ECR
* Builds and tags your docker image, with the tag based on the GitLab CI Pipeline execution id.
* Pushes your docker image to ECR

### Create an IAM user to support push to ECR
Prerequisite - A repository in ECR must have been created before proceeding with the next steps.
Login to AWS console using JIT process, and create a user with permission AmazonEC2ContainerRegistryPowerUser. It can be done by logging in to AWS console(refer [JIT Access](https://docs.duplocloud.com/docs/aws/use-cases/jit-access)) and navigating to Services > Security, Identity and Compliance > IAM > Users and then following the on screen steps. Select **Access key - Programmatic access** in first step while creating the user , and assign a policy named **AmazonEC2ContainerRegistryPowerUser** direclty in the second step. This policy allows this user to list, read and write the images in the repository. The final step of the user creation process will have an option to download the access credentials. Please download and save the csv.

Go to GitLab > Settings > CI CD > Variables > Expand and set the follwing additional variables.
AWS_DEFAULT_REGION
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY


### Example Workflow

Here is an example gitlab workflow that builds a docker image and pushes it to DockerHub.

To use it you will need to change:

* `DOCKER_REGISTRY`variable
* `AWS_DEFAULT_REGION`variable
* `APP_NAME`variable

```yaml
variables:
  DOCKER_REGISTRY: XXXXXXXXXX.dkr.ecr.<region>.amazonaws.com  #Change It
  AWS_DEFAULT_REGION: <region>                                #Change It
  APP_NAME: <container name>                                  #Change It
  DOCKER_HOST: tcp://docker:2375

stages:
  - build
  - deploy

build-and-push-job:
  stage: build
  image:
    name: amazon/aws-cli                                     #Base image, needed for AWS CLI tools
    entrypoint: [""]
  services:
    - docker:dind                                            #Docker In Docker - needed for docker commands
  before_script:
    - amazon-linux-extras install docker
    - aws --version
    - docker --version
  script:
    - |
      tag="$CI_PIPELINE_IID"
      echo "Running on branch '$CI_COMMIT_BRANCH': tag = $tag"
    - docker build -t "$DOCKER_REGISTRY/$APP_NAME:${tag}" . # Replace . with path to Dockerfile relative to this file if Dockerfile is not in repo root dir
    - aws ecr get-login-password | docker login --username AWS --password-stdin $DOCKER_REGISTRY
    - docker push "$DOCKER_REGISTRY/$APP_NAME:${tag}"
    - docker logout #For security
```
