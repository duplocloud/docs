---
description: >-
  One agent that provisions, operates and troubleshoots cloud infrastructure on
  AWS, Azure and Oracle Cloud, with Google Cloud coming soon.
icon: robot
---

# Infrastructure Agent

The Infrastructure Agent manages your cloud infrastructure from end to end. You describe what you want, such as a network, a Kubernetes cluster, or a database, and the agent provisions it, reports back, and keeps it in step with your request. You can also connect infrastructure you already run, then operate and troubleshoot it with AI.

It's one agent for every supported cloud. You pick the cloud when you create a network, and everything you build on that network uses the same resource model, statuses and approval flow.

{% hint style="info" %}
In the portal, this agent's section of the left nav is being renamed from **DevOps** to **Infrastructure Agent**. Until your portal has the update, look for **DevOps**.
{% endhint %}

## Supported clouds

| Cloud | Kubernetes | Status | Step-by-step guide |
| --- | --- | --- | --- |
| **AWS** | Amazon EKS | Supported | [Get Started on AWS](quick-start/README.md) |
| **Azure** | Azure Kubernetes Service (AKS) | Supported | Coming soon |
| **Oracle Cloud (OCI)** | Oracle Kubernetes Engine (OKE) | Supported | Coming soon |
| **Google Cloud (GCP)** | Google Kubernetes Engine (GKE) | Coming soon | Coming soon |

The [Policy Model](policy-model/README.md) pages apply to every cloud and note where a cloud works differently. The walkthroughs and examples are written for AWS for now.

## What you can do

* **Connect existing infrastructure.** Attach your cloud accounts as Providers and start using AI to operate, troubleshoot and optimize what's already running.
* **Provision new infrastructure.** Create networks, Kubernetes clusters and environments through structured forms. The agent provisions them and reports the results.
* **Deploy and manage applications.** Create Kubernetes workloads, namespaces, secrets and managed databases inside your environments.
* **Customize to your standards.** Override the default provisioning skills with your own to enforce tagging policies, compliance requirements or architectural patterns.

## Sections

<table data-view="cards"><thead><tr><th>Title</th><th>Description</th><th data-card-target data-type="content-ref">Target</th></tr></thead><tbody><tr><td><strong>Policy Model</strong></td><td>The resources the agent manages, on every cloud, and how they relate.</td><td><a href="policy-model/">policy-model</a></td></tr><tr><td><strong>Installation</strong></td><td>Deploy DuploCloud to your cloud and connect your accounts.</td><td><a href="installation.md">installation.md</a></td></tr><tr><td><strong>Customizing the Agent</strong></td><td>Override default skills to match your organization's standards.</td><td><a href="customizing/">customizing</a></td></tr><tr><td><strong>Get Started on AWS</strong></td><td>Connect existing AWS infrastructure, or provision new infrastructure step by step.</td><td><a href="quick-start/">quick-start</a></td></tr></tbody></table>
