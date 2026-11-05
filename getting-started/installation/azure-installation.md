---
description: Azure support for Cloud Deploys is coming soon. What to expect and where the Terraform lives.
---

# Azure

{% hint style="warning" %}
**Coming soon.** Cloud Deploys does not support Azure yet. In the wizard, **Microsoft Azure** appears disabled with a **Coming soon** label.
{% endhint %}

When Azure is available, Cloud Deploys will deploy the portal onto Azure Kubernetes Service (AKS) in your Azure subscription, with the same wizard and plan review as [AWS](aws-installation.md).

***

## Prerequisites

| Item | Notes |
| --- | --- |
| **A connected Azure provider** | Attached to your workspace in the DevKit. |
| **Permissions** | Contributor on the subscription or resource group you deploy into, and cluster-admin on the cluster if you use an existing AKS cluster. |
| **A hostname and certificate** | A DNS name for the portal and a way to issue a TLS certificate for it. |

***

## What is created

The deployment will include an AKS cluster (or your existing one), shared file storage, an ingress controller, workload identity for the portal's services, and the portal itself installed with its Helm chart.

***

## The Terraform behind it

TODO(link): Azure Terraform repository README (repo is being made public; master to supply the URL).

Until Azure is supported in Cloud Deploys, you can install the portal on an existing AKS cluster with the [Systems Integrator Installation Guide](systems-integrator-installation-guide.md), or ask your DuploCloud contact about a deployment done for you.
