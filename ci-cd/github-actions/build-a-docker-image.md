---
description: Use Duplo to build and push a docker image from Github Actions
---

# Build a docker image

{% hint style="info" %}
Avoid using capital letters when referencing a DuploCloud construct, such as a Tenant, even when the UI displays the string as all capital letters. Don't specify **DEV01** for example, specify **dev01**.
{% endhint %}

## Build and Push to ECR

The goal of this section is to show how you can build a docker image and push it to ECR.

It does three basic things:

* Logs in to AWS ECR (using just-in-time AWS credentials from Duplo)
* Builds and tags your docker image, with the tag based on the git commit SHA.
* Pushes your docker image

### Example Workflow

Here is an example github workflow that builds a docker image and pushes it to ECR.

To use it you will need to change:

* `duplo_host` env var
* _`<SERVICE_NAME>`_ env var
* _`<TENANT_NAME>`_ env var

```yaml
name: Build and Deploy
on:
  # (Optional) Allows users to trigger the workflow manually from the GitHub UI
  workflow_dispatch:

  # Triggers the workflow on push to matching branches
  push:
    branches:
      - master
env:
  duplo_host: https://mysystem.duplocloud.net  # CHANGE ME!
  duplo_token: "${{ secrets.DUPLO_TOKEN }}"
  SERVICE_NAME: myservice                      # CHANGE ME!
  TENANT_NAME: mytenant                        # CHANGE ME!

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      # Set up for docker build
      - name: Get AWS credentials
        uses: duplocloud/ghactions-aws-jit@master
        with:
          tenant: default
      - name: Login to Amazon ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@v1

      # Build and push the docker image
      - name: Docker Build and Push
        uses: docker/build-push-action@v4
        with:
          context: .
          push: true
          tags: |
            ${{ steps.login-ecr.outputs.registry }}/${{ env.SERVICE_NAME }}:${{ github.sha }}
            
    # This part is important - it will be used by the deploy job
    outputs:
      image: "${{ steps.login-ecr.outputs.registry }}/${{ env.SERVICE_NAME }}:${{ github.sha }}"
```
