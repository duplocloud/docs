---
description: Use Duplo to build and push a docker image from Github Actions
---

# Build a Docker image

{% hint style="info" %}
Avoid using capital letters when referencing a DuploCloud construct, such as a Tenant, even when the UI displays the string as all capital letters. Don't specify **DEV01** for example, specify **dev01**.
{% endhint %}

## Build and Push to ECR

The goal of this section is to show how you can build a docker image and push it to ECR.

It does three basic things:

* Logs in to AWS ECR (using just-in-time AWS credentials from Duplo)
* Builds and tags your docker image, with the tag based on the git commit SHA and ref.
* Pushes your docker image

### Example Workflow

Here is an example github workflow that builds a docker image and pushes it to ECR.

To use it you will need to ensure the following are configured correctly:

* `DUPLO_HOST` env var
* `DUPLO_TOKEN` env var

<pre class="language-yaml"><code class="lang-yaml">name: Publish Image
on:
  # Triggers the workflow on push to matching branches
  push:
    branches:
    - main
  # (Optional) Allows users to trigger the workflow manually from the GitHub UI
  workflow_dispatch: {}
  # (Optional) Allow other workflows to use this workflow ant its outputs
  workflow_call: 
    outputs:
      image:
        description: The URI of the image
        value: ${{ jobs.build_image.outputs.image }}
    secrets:
      DUPLO_TOKEN:
        description: The token to use for Duplo API calls
        required: true

env:
  DUPLO_HOST: ${{ vars.DUPLO_HOST }}
  DUPLO_TOKEN: ${{ secrets.DUPLO_TOKEN }}
  # Images are usually stored in a dediacted tenant, so the name doesn't change
  DUPLO_TENANT: devops

jobs:
  build_image:
    name: Build and Push Image
    runs-on: ubuntu-latest
    outputs:
      image: ${{ steps.build_image.outputs.uri }}
    steps:

    - name: Checkout code
      uses: actions/checkout@v4

    # configures duplocloud and host cloud, eg aws
    - name: Cloud CI Setup
      uses: <a data-footnote-ref href="#user-content-fn-1">duplocloud/actions/setup@</a>v0.0.5
    
    # logs into registry, configures docker, builds image, lastly pushes
    - name: Build and Push Docker Image
      id: build_image
      uses: <a data-footnote-ref href="#user-content-fn-2">duplocloud/actions/build-image@</a>v0.0.5
      with:
        platforms: linux/amd64,linux/arm64
        push: true # false for dry runs
        build-args: >
          foo=bar
          ice_cream=chocolate
          name=${{ github.repository }}
</code></pre>

### References

* [Duplocloud Build Image Action for Github](https://github.com/duplocloud/actions/tree/main/build-image)
* [NPM Pipeline Example using this workflow](https://github.com/duplocloud/npm-pipeline-example/tree/main/.github/workflows)
* [Github on Publishing Docker Images](https://docs.github.com/en/actions/publishing-packages/publishing-docker-images)
* [Dockers Introduction to GitHub Actions](https://docs.docker.com/build/ci/github-actions/)

[^1]: [https://github.com/duplocloud/actions/tree/main/setup](https://github.com/duplocloud/actions/tree/main/setup)

[^2]: [https://github.com/duplocloud/actions/tree/main/build-image](https://github.com/duplocloud/actions/tree/main/build-image)
