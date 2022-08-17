---
description: Use Duplo to build and push a docker image from Gitlab CI/CD
---

# Build a docker image

## Build and Push to DockerHub

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
