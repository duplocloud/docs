---
description: Google Cloud support for Cloud Deploys is coming soon. What to expect and where the Terraform lives.
---

# GCP

{% hint style="warning" %}
**Coming soon.** Cloud Deploys does not support Google Cloud yet. In the wizard, **Google Cloud** appears disabled with a **Coming soon** label.
{% endhint %}

When Google Cloud is available, Cloud Deploys will deploy the portal onto Google Kubernetes Engine (GKE) in your project, with the same wizard and plan review as [AWS](aws-installation.md).

***

## Prerequisites

| Item | Notes |
| --- | --- |
| **A connected Google Cloud provider** | Attached to your workspace in the DevKit. |
| **Permissions** | Permission to create and manage GKE, networking and storage resources in your project. |
| **A hostname and certificate** | A DNS name for the portal and a way to issue a TLS certificate for it. |

***

## What is created

The deployment will include a GKE cluster (or your existing one), shared file storage, an ingress controller, workload identity for the portal's services, and the portal itself installed with its Helm chart.

***

## The Terraform behind it

The Google Cloud Terraform is public: [duplocloud/helpdesk-gcp](https://github.com/duplocloud/helpdesk-gcp). Its README describes the resources and variables.

Until Google Cloud is supported in Cloud Deploys, you can install the portal on an existing GKE cluster with the [Systems Integrator Installation Guide](systems-integrator-installation-guide.md), or ask your DuploCloud contact about a deployment done for you.
