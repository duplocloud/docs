---
description: Install the DevKit, try a ready-made agent, then build your own. Start here.
---

# Quick Start

The Quick Start takes you from nothing to a working agent in three steps. Most people only need this section.

{% stepper %}
{% step %}
## Install the DevKit

The DevKit runs the whole DuploCloud platform on your own machine. You connect a cloud account to it and run agents there before anything touches production. See [Install the DevKit](install-the-devkit.md).
{% endstep %}

{% step %}
## Try a ready-made agent

Activate an agent from the Agent Marketplace, connect it to your cloud account, and see its results. See [Try a Marketplace Agent](try-a-marketplace-agent.md).
{% endstep %}

{% step %}
## Build your own agent

Pick the platform you work on (AWS, Azure, GCP, Kubernetes, Git, or another tool) and follow a worked example that ends in an agent you built yourself. See [Build Your Own Agent](build-your-own-agent/README.md).
{% endstep %}
{% endstepper %}

## Two ways in

| Start here | What it's for |
| --- | --- |
| **DevKit** (recommended) | Run the platform on your laptop, connect a cloud account, and try or build agents. The first run gets you a trial license. See [Install the DevKit](install-the-devkit.md). |
| [**Agent Marketplace**](https://marketplace.duplocloud.com) | Browse the agents DuploCloud publishes, both included and paid, before you install anything. You activate agents from inside your portal. See [Agent Marketplace and Buying Agents](marketplace.md). |

{% hint style="info" %}
**DevOps engineer who wants to skip the DevKit?** You can install the DuploCloud portal straight into your own cloud with Terraform or Helm. See [Deploy to Your Cloud](deploy-to-your-cloud.md).
{% endhint %}

## When you're ready for your team

The DevKit runs on your machine only. To give your team a shared portal in your own cloud account, see [Deploy to Your Cloud](deploy-to-your-cloud.md).

## Free and paid

A **free** license gets you a trial for building locally in the DevKit and one environment in your own cloud. Free licenses have limits on users, workspaces, providers and agents. A **paid** license lifts those limits. See [Licensing](licensing.md).
