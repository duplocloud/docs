---
description: Configure GitHub to integrate with DuploCloud
---

# Configure GitHub

## Prerequisites

**Deploy and test the application** - To use GitHub CI/CD, deploy your application with DuploCloud as a Service and test that it works as expected.

[**Add Google Cloud Credentials**](../../gcp/gcp-services/cloud-credentials.md) - Add a Service Account, setting up Cloud Credentials for GCP in DuploCloud.

{% hint style="info" %}
GitHub CI/CD is recommended only for upgrades of container images and to run tests that can be written before or after the upgrade.
{% endhint %}

## Obtaining and configuring an API token

To call a DuploCloud API from Github, obtain an [API token](../../user-administration/access-control/api-tokens.md).

1. Create a Service Account user in DuploCloud. Service Account users are usernames that are not an email address, such as `github-bot` or `my-api-user`. These users do not log in, but their account owns the API token.
2. Give the DuploCloud user access to the desired Tenant. See [adding Tenant access for a user](../../user-administration/access-control/tenant-access/#adding-tenant-access-for-a-user).
3. Create an API token for that user. See [creating API Tokens](../../user-administration/access-control/api-tokens.md).
4. Add a [GitHub Repository secret](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions) that contains the DuploCloud API token.

## Adding Tenant access for users

{% content-ref url="../../user-administration/access-control/tenant-access/" %}
[tenant-access](../../user-administration/access-control/tenant-access/)
{% endcontent-ref %}

![](<../../.gitbook/assets/Screen Shot 2022-02-24 at 2.32.57 PM.png>)

## GCP Security Account

When using GCP with a dedicated security account for pipeline access, you must make it available to the pipelines.&#x20;

### Creating the Service Account for GCP

1. [Navigate to obtain GCP credentials](https://console.cloud.google.com/apis/credentials).
2. Select the project.
3. [Create a Service Account](https://cloud.google.com/iam/docs/service-accounts-create).
4. Create a key for the Service Account and download the JSON credentials for use in GitHub Actions.
5. In GitHub, navigate to **Settings**.
6. Create a GitHub Actions Secret named `CLOUD_CREDENTIALS` with the contents pasted from the JSON credentials you downloaded from the Service Account.
7. Create a GitHub Actions Variable named `CLOUD_ACCOUNT` with the Project ID or Name from GCP.&#x20;

The JSON Credentials file you download has the following content:&#x20;

{% code title="GCP JSON Credentials file" %}
```json
{
  "type": "service_account",
  "project_id": "<project-id>",
  "private_key_id": "<private-key-id>",
  "private_key": "<private-key>",
  "client_email": "<client-email>",
  "client_id": "<client-id>",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://accounts.google.com/o/oauth2/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "<client-x509-cert-url>"
}
```
{% endcode %}

### Azure Security Account

Create an Azure Security Account with needed permissions in Azure Entra ID.&#x20;

The JSON Credential file has the following content:&#x20;

{% code title="Azure JSON Credentials file" %}
```json
{
  "clientId": "<client-id>",
  "clientSecret": "<client-secret>",
  "subscriptionId": "<subscription-id>",
  "tenantId": "<tenant-id>"
}
```
{% endcode %}

\
Within Github Actions Settings

* Create a Github Actions Secret named `CLOUD_CREDENTIALS` with the contents pasted from the json credentials you downloaded from the service account
* Create a Github Actions Variable named `CLOUD_ACCOUNT` with the directory name for Azure.&#x20;

### Setup Duplocloud in a Workflow

To get fully setup with Duplocloud and the underlying cloud provider you use, you get everything you need setup with [duplocloud/actions/setup](https://github.com/duplocloud/actions/tree/main/setup). This action will install the cli for duplocloud and the CLI for the underlying cloud as well. Finally it will perform a safe login so subsequent steps may freely interact with duplocloud or the cloud it manages.&#x20;

Here is the most basic setup for any pipeline to get started.&#x20;

<pre class="language-yaml"><code class="lang-yaml">jobs:
  build:
    runs-on: ubuntu-latest
    env:
      DUPLO_TOKEN: ${{ secrets.DUPLO_TOKEN }}
      DUPLO_HOST: ${{ vars.DUPLO_HOST  }}
      DUPLO_TENANT: ${{ vars.DUPLO_TENANT }}
    steps:
    - name: Duplo Setup
      uses: <a data-footnote-ref href="#user-content-fn-1">duplocloud/actions/setup@v0.0.</a>5
      with: # these are only needed for GCP and Azure
        account-id: ${{ vars.CLOUD_ACCOUNT }}
        credentials: ${{ secrets.CLOUD_CREDENTIALS }}
</code></pre>

### Configuring Environments for Github Actions

[Github Environments](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment) are how you define different deployment environments for your workflows and how they are differ from one to the other. Here you define environment specific variables and secrets. This allows you to parameterize and secure your workflows.  We highly recommend using this feature, however it is paid and therefore optional since you may not have it.&#x20;

The most common use case with Duplocloud is to match up one Tenant to one Environment. Imagine we have a tenant named `dev01`, then you make a new environment in _every_ repo which will deploy to it named `dev01`. Often times you may not even need to add any secrets or variables because we already added the `DUPLO_HOST` and `DUPLO_TOKEN` at the repo level earlier and you only need the name of the environment as the value for the `DUPLO_TENANT`.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-01 at 3.46.14 PM.png" alt=""><figcaption><p>Environments Management in Github Repo Settings page</p></figcaption></figure>

This shows how to configure a job to use an environment using an input and match it up to the tenant.&#x20;

<pre class="language-yaml"><code class="lang-yaml">name: My Workflow
on: 
  workflow_dispatch:
    inputs:
      environment:
        description: The environment to deploy to
        type: environment
        default: dev01
jobs:
  build:
    runs-on: ubuntu-latest
    environment:
      name: ${{ inputs.environment }}
    env:
      DUPLO_TOKEN: ${{ secrets.DUPLO_TOKEN }}
      DUPLO_HOST: ${{ vars.DUPLO_HOST  }}
      DUPLO_TENANT: ${{ inputs.environment }}
    steps:
    - name: Duplo Setup
      uses: <a data-footnote-ref href="#user-content-fn-2">duplocloud/actions/setup@v0.0.</a>5
      with: # these are only needed for GCP and Azure
        account-id: ${{ vars.CLOUD_ACCOUNT }}
        credentials: ${{ secrets.CLOUD_CREDENTIALS }}
</code></pre>

The input type is `environment` which only works on `workflow_dispatch` because it provides a UI with a drop down selector for choosing from the list of configured Github Environments.  On any other event type, the environment input would simply be type string and you pass in a name. \


<figure><img src="../../.gitbook/assets/Screenshot 2024-04-01 at 3.36.56 PM (1).png" alt=""><figcaption><p>Environment Selector in workflow dispatch UI</p></figcaption></figure>

References:

* [Create and delete service account keys](https://cloud.google.com/iam/docs/keys-create-delete)
* [Github Using environments for deployment](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment)



{% hint style="warning" %}
The rest of this documentation will assume that you named the GitHub repository secret `DUPLO_TOKEN`.
{% endhint %}

[^1]: [https://github.com/duplocloud/actions/tree/main/setup](https://github.com/duplocloud/actions/tree/main/setup)

[^2]: [https://github.com/duplocloud/actions/tree/main/setup](https://github.com/duplocloud/actions/tree/main/setup)
