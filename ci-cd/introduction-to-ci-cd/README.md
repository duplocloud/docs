---
description: >-
  Ensuring continuous integration, delivery, and deployment of your Cloud
  applications
coverY: 0
---

# CI/CD Overview

DuploCloud supports all available CI/CD platforms, including some of the most popular such as GitHub Actions, CircleCI, and GitLab. Duplocloud has a brand agnostic view of CI/CD which revolves around having great support for our client tools and integrating them into the popular brands for a native and intuitive feel no matter the tool you choose.&#x20;

In addition to third-party CI/CD products, DuploCloud provides [Katkit](../katkit/), a built-in CI/CD platform that allows you to build, test, and deploy your application from GitHub commits and pull requests. Katkit is an arbitrary code execution engine that allows you to run any code before and after deployment. Conforming to DuploCloud's architecture, Katkit uses [Tenants](../../getting-started/application-focussed-interface/tenant/), tying together CI and CD.

No matter the brand of tool you use, they all need secure access to your Duplocloud Portal using some credentials attached to a service account.&#x20;

{% content-ref url="service-accounts.md" %}
[service-accounts.md](service-accounts.md)
{% endcontent-ref %}

Once you have a service account properly setup for your cloud, then you configure those credentials with the tool itself. Some of the CI/CD toolchains that are directly supported by DuploCloud include, but are not limited, to the following:

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><a href="../github-actions/"><strong>GitHub Actions</strong></a></td><td>Documentation guides for getting started using CI/CD with GitHub Actions</td><td><a href="../github-actions/">github-actions</a></td></tr><tr><td><a href="../circleci/"><strong>CircleCI</strong></a></td><td>Documentation guides for getting started using CI/CD with CircleCI</td><td><a href="../circleci/">circleci</a></td></tr><tr><td><a href="../gitlab-ci-cd/"><strong>GitLab CI/CD</strong></a></td><td>Documentation guides for getting started using CI/CD with GitLab CI/CD</td><td><a href="../gitlab-ci-cd/">gitlab-ci-cd</a></td></tr><tr><td><a href="../bitbucket-pipelines/"><strong>BitBucket Pipelines</strong></a></td><td>Documentation guides for getting started with BitBucket Pipelines</td><td></td></tr><tr><td><a href="../azure-pipelines/"><strong>Azure DevOps</strong></a></td><td>Documentation guides for getting started with Azure DevOps</td><td></td></tr><tr><td><a href="../katkit/"><strong>Katkit</strong></a></td><td>Documentation guides for getting started using CI/CD with Katkit</td><td><a href="../katkit/">katkit</a></td></tr></tbody></table>
