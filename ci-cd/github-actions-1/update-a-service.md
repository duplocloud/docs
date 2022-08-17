---
description: Use Duplo to update a service's container from Gitlab CI/CD
---

# Update a service

## Update the docker image for a service

The goal of this section is to show how you can update the docker image for a service, after you have built that image.

### Example Workflow

This example makes some assumptions:

* Your workflow already has a `build` job - we created one in the previous section



```yaml
variables:
  DOCKERHUB_USERNAME: duplocloud               # CHANGE ME!
  DOCKERHUB_REPO: mydockerhubid/myrepo         # CHANGE ME!
  DUPLO_HOST: https://mysystem.duplocloud.net  # CHANGE ME!
  DUPLO_SERVICE_NAME: myservice                # CHANGE ME!
  TENANT_NAME: mytenant

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
docker-deploy:
  # Use the official docker image.
  image: docker:latest
  stage: deploy
  services:
    - docker:dind
  before_script:
    - apk add --update curl jq && rm -rf /var/cache/apk/*
  script:
    - |
      tag=":$CI_COMMIT_SHA"
      wget https://raw.githubusercontent.com/duplocloud/demo-npm-service/master/.circleci/duplo_utils.sh
      chmod +x duplo_utils.sh
      source duplo_utils.sh
      update_service_api $(get_tenant_id $TENANT_NAME) "$DOCKERHUB_REPO${tag}"
```
