---
description: Connect DuploCloud to your AWS accounts and cloud providers.
---

# Installation

Before using the AWS Extension, you need to install DuploCloud in your cloud environment and connect it to your AWS accounts and any additional providers you want the AI to access.

## Steps

{% stepper %}
{% step %}
### Install DuploCloud on AWS

Follow the AWS installation guide to deploy DuploCloud into your AWS account.

{% content-ref url="../../getting-started/installation/aws-installation.md" %}
[aws-installation.md](../../getting-started/installation/aws-installation.md)
{% endcontent-ref %}
{% endstep %}

{% step %}
### Connect Cloud Providers

Connect your AWS accounts, Kubernetes clusters, Git repositories, and other systems as Providers. Each Provider gives the AI scoped access to the resources inside it.

{% content-ref url="../../getting-started/integrating-providers/" %}
[integrating-providers](../../getting-started/integrating-providers/)
{% endcontent-ref %}
{% endstep %}

{% step %}
### Connect MCP Servers

{% hint style="info" %}
This step is optional. Connect MCP Servers if you want to extend the AI's access to external tools and APIs — such as monitoring platforms, ticketing systems, or CI/CD pipelines.
{% endhint %}

{% content-ref url="../../getting-started/integrating-mcp-servers/" %}
[integrating-mcp-servers](../../getting-started/integrating-mcp-servers/)
{% endcontent-ref %}
{% endstep %}
{% endstepper %}
