---
description: Use Duplo to update a Service container from Github Actions
---

# Update a Kubernetes Service

## Update the docker image for a service

The goal of this section is to show how you can update the docker image for a Kubernetes service, after you have built that image. This task can be achieved using the [duplocloud/actions/update-image](https://github.com/duplocloud/actions/tree/main/update-image) action.&#x20;

### Example Workflow

This example makes some assumptions:

* Your workflow already has a `build` job - we created one in the previous section
* Your `build` job declares an output named `image` - also done in the previous section

To use it you will need to ensure your GHA Environment has the following:

* `DUPLO_HOST` env var
* `DUPLO_TENANT` env var
* `DUPLO_TOKEN` env var

You need to change the service name below from `my-service` to the name of your actual service.&#x20;

<pre class="language-yaml"><code class="lang-yaml">name: Update Service

on: 
  workflow_dispatch:
    inputs:
      environment:
        description: The environment to deploy to
        type: environment
        default: dev
        required: true
      image:
        description: The full image
        type: string
        required: true

jobs:
  update_service:
    name: Update Service
    runs-on: ubuntu-latest
    environment: 
      name: ${{ inputs.environment }}
    env:
      DUPLO_TOKEN: ${{ secrets.DUPLO_TOKEN }}
      DUPLO_HOST: ${{ vars.DUPLO_HOST  }}
      DUPLO_TENANT: ${{ vars.DUPLO_TENANT }}
    steps: 
    
    # install and login to the cloud
    - name: Duplo Setup
      uses: <a data-footnote-ref href="#user-content-fn-1">duplocloud/actions@v0.0.12</a>
      # only required on gcp and azure
      with:
        account-id: ${{ vars.CLOUD_ACCOUNT }}
        credentials: ${{ secrets.CLOUD_CREDENTIALS }}

    # uses duploctl from above
    - name: Update Service
      uses: duplocloud/actions/update-image@v0.0.5
      with:
        name: my-service
        image: ${{ inputs.image }}
        type: service
</code></pre>

[^1]: [https://github.com/duplocloud/actions](https://github.com/duplocloud/actions)
