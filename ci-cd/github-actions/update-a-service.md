---
description: Use Duplo to update a Service container from Github Actions
---

# Update a Service

## Update the docker image for a service

The goal of this section is to show how you can update the docker image for a service, after you have built that image. This task can be achieved using the [duplocloud/actions/update-service](https://github.com/duplocloud/actions/tree/main/update-service) action.&#x20;

### Example Workflow

This example makes some assumptions:

* Your workflow already has a `build` job - we created one in the previous section
* Your `build` job declares an output named `image` - also done in the previous section

To use it you will need to change:

* `DUPLO_HOST` env var
* `SERVICE_NAME` env var
* `TENANT_NAME` env var

```yaml
name: Update Service

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
      uses: duplocloud/actions/setup@v0.0.3
      # only required on gcp and azure
      with:
        account-id: ${{ vars.CLOUD_ACCOUNT }}
        credentials: ${{ secrets.CLOUD_CREDENTIALS }}

    # uses duploctl from above
    - name: Update Service
      uses: duplocloud/actions/update-service@v0.0.3
      with:
        service: my-service
        image: ${{ inputs.image }}
```
