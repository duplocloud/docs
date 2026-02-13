---
description: >-
  Ensuring continuous integration, delivery, and deployment of your Cloud
  applications
cover: ../../.gitbook/assets/banner dark.png
coverY: 0
---

# CI/CD Overview

DuploCloud supports all available CI/CD platforms, including some of the most popular such as GitHub Actions, CircleCI, and GitLab. Duplocloud has a brand agnostic view of CI/CD which revolves around having great support for our client tools and integrating them into the popular brands for a native and intuitive feel no matter the tool you choose.&#x20;

In addition to third-party CI/CD products, DuploCloud provides [Katkit](katkit/), a built-in CI/CD platform that allows you to build, test, and deploy your application from GitHub commits and pull requests. Katkit is an arbitrary code execution engine that allows you to run any code before and after deployment. Conforming to DuploCloud's architecture, Katkit uses [Tenants](../application-focused-interface-duplocloud-architecture/tenant.md), tying together CI and CD.

No matter the brand of tool you use, they all need secure access to your Duplocloud Portal using some credentials attached to a service account.&#x20;

{% content-ref url="service-accounts.md" %}
[service-accounts.md](service-accounts.md)
{% endcontent-ref %}

## DuploCloud CI/CD integrations

DuploCloud’s CI/CD integrations are crucial in orchestrating cloud code deployments by seamlessly connecting your existing CI/CD platforms with the DuploCloud Platform. Here’s how it works:

CI/CD systems like GitHub Actions, GitLab, and Azure DevOps can leverage DuploCloud’s prepackaged libraries and modules to invoke DuploCloud functionality directly from their pipelines. This allows you to automate the deployment of your cloud infrastructure and applications, ensuring continuous integration, delivery, and deployment.

Some key integration points between CI/CD systems and DuploCloud include:

1. Cloud Access for Hosted Runners: DuploCloud provides just-in-time (JIT) access scoped to Tenants for CI/CD build pipelines. Users can create a "CICD" user in the DuploCloud portal with limited access to the desired Tenants, and a token is generated for the user to be added to the CI/CD pipelines.
2. Deploying Self-Hosted Runners within the Tenant: DuploCloud allows you to deploy a set of build containers within the same Tenant as the application, enabling the build to seamlessly access the Tenant's resources like Docker registries, internal APIs, object stores, SQL, etc.
3. AWS SecurityHub and Azure Defender Integration: DuploCloud integrates natively with cloud provider-native security solutions like AWS Security Hub and Azure Defender, handling the setup, management, and operations.

Once you have a service account properly set up for your cloud, you can configure those credentials with the tool. Some of the CI/CD integrations that are directly supported by DuploCloud include:

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><a href="github-actions/"><strong>GitHub Actions</strong></a></td><td>Documentation guides for getting started using CI/CD with GitHub Actions</td><td><a href="github-actions/">github-actions</a></td></tr><tr><td><a href="circleci/"><strong>CircleCI</strong></a></td><td>Documentation guides for getting started using CI/CD with CircleCI</td><td><a href="circleci/">circleci</a></td></tr><tr><td><a href="gitlab-ci-cd/"><strong>GitLab CI/CD</strong></a></td><td>Documentation guides for getting started using CI/CD with GitLab CI/CD</td><td><a href="gitlab-ci-cd/">gitlab-ci-cd</a></td></tr><tr><td><a href="bitbucket-pipelines/"><strong>BitBucket Pipelines</strong></a></td><td>Documentation guides for getting started with BitBucket Pipelines</td><td></td></tr><tr><td><a href="azure-pipelines/"><strong>Azure DevOps</strong></a></td><td>Documentation guides for getting started with Azure DevOps</td><td></td></tr><tr><td><a href="katkit/"><strong>Katkit</strong></a></td><td>Documentation guides for getting started using CI/CD with Katkit</td><td><a href="katkit/">katkit</a></td></tr><tr><td><a href="argocd.md">ArgoCD</a></td><td>Documentation guides for getting started with ArgoCD integrations</td><td></td></tr></tbody></table>
