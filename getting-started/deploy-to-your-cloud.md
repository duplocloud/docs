---
description: Move from the DevKit on your laptop to your own DuploCloud portal in your cloud account, so your whole team can use your agents.
---

# Deploy to Your Cloud

The DevKit is for you, on your own machine. When you want your team to use your agents, run the platform in your own cloud account as a **portal**. Each portal is one **environment**: a named deployment with its own license.

{% stepper %}
{% step %}
## Create an environment

Register the environment in the DuploCloud Console, which gives it its license. The Cloud Deployment Agent can do this for you. See [Create an Environment](create-an-environment.md).
{% endstep %}

{% step %}
## Deploy your portal with the Cloud Deployment Agent

From the DevKit, the Cloud Deployment Agent creates your portal in your cloud account. You review exactly what it will create before you approve it. See [Cloud Deployment Agent](installation/README.md).
{% endstep %}

{% step %}
## Add your agents

Activate agents from the Marketplace in your new portal, or deploy the agents you built in the DevKit. See [Marketplace Agents](../marketplace-agents/README.md) and [Deploy Your Own Agents](deploy-your-own-agents.md).
{% endstep %}
{% endstepper %}

{% hint style="info" %}
**Prefer Terraform or Helm?** Install the portal yourself:

* AWS: [terraform-aws-helpdesk](https://github.com/duplocloud/terraform-aws-helpdesk)
* Azure: [helpdesk-deployer-azure](https://github.com/duplocloud-internal/helpdesk-deployer-azure)
* GCP: [helpdesk-gcp](https://github.com/duplocloud/helpdesk-gcp)
* Any Kubernetes cluster, with the Helm chart: [Systems Integrator Installation Guide](installation/systems-integrator-installation-guide.md)

DuploCloud may also deploy the portal for you, case by case. Ask your DuploCloud contact.
{% endhint %}
