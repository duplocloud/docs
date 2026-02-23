---
description: Use Duplo to update a Service container from Github Actions
---

# Update a Kubernetes Service

Update the Docker image for a Kubernetes service after building a new version. This can be done automatically for the main container using CI/CD workflows. For init and sidecar containers, image updates require using the API directly, supporting more complex deployment scenarios.

## Updating the docker image for a service

Use a GitHub Actions workflow to update the Docker image for the main container in your Kubernetes service. This simplifies deployment as part of your CI/CD process.

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

## Updating Init or Sidecar Container Images

Update images for [init and sidecar containers](../../automation-platform/kubernetes-overview/initcontainers-and-sidecar-containers.md) by calling the DuploCloud API directly. This supports more advanced deployment scenarios beyond updating just the main container.

To update images for these container types, use the following API:

### **Endpoint** `PUT /v3/subscriptions/{tenant}/containers/replicationController/{k8sservicename}/containerimage`

### **Authorization**

Use a valid API token (`Bearer {token}`) in the Authorization header. You can generate a permanent API token from the DuploCloud Portal: see the [API Token](../../access-control/api-tokens.md#permanent-api-tokens) page for instructions.

### **Request Body Format**

Submit a JSON array with one or more objects containing:

* `ContainerName`: The exact name of the container (e.g., main, init, or sidecar container)
* `ImageName`: The new image to use

### **Example Workflow**

```json
jsonCopyEdit[
  {
    "ContainerName": "duplo-main-container",
    "ImageName": "mycompany/app:latest"
  },
  {
    "ContainerName": "init-migrator",
    "ImageName": "mycompany/db-migrator:2.0"
  },
  {
    "ContainerName": "logging-sidecar",
    "ImageName": "mycompany/logs-agent:1.3"
  }
]
```

{% hint style="warning" %}
The `duplocloud/actions/update-image` GitHub Action currently only supports updating the main container. To update init or sidecar containers, call the API directly within a script or CI/CD step (for example, using `curl`). \
\
Make sure the `ContainerName` exactly matches the name defined for the init or additional containers in your service configuration.
{% endhint %}

[^1]: [https://github.com/duplocloud/actions](https://github.com/duplocloud/actions)
