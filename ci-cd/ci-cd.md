---
description: >-
  Ensuring continuous integration, delivery, and deployment of your Cloud
  applications
---

# CI/CD

Continuous Integration and Deployment (CI/CD) is a software development practice in Cloud computing that ensures the rapid development, integration, and deployment of applications, using multiple pipelines, for a consistent, quality-focused approach.&#x20;

There are several CI/CD-based platforms that you can use to ensure that your applications work as expected in both local and test environments on a repeatable basis. As DuploCloud treats CI/CD platforms agnostically through the use of [cURL commands](https://en.wikipedia.org/wiki/CURL), it supports most available CI/CD platforms.

In addition to third-party CI/CD products, DuploCloud provides [KatKit](katkit/), a built-in CI/CD platform that allows you to build, test, and deploy your application from GitHub commits and pull requests. Katkit is an arbitrary code execution engine that allows you to run any code before and after deployment. Conforming to DuploCloud's architecture, Katkit uses [Tenants](../getting-started/application-focussed-interface/tenant.md), tying together CI and CD.&#x20;

In addition to KatKit, some of the CI/CD platforms that DuploCloud supports, but are not limited to supporting, are:

* Azure DevOps
* [CircleCI](circleci/)
* [GitHub](github-actions/)
* [GitLab](github-actions-1/)



