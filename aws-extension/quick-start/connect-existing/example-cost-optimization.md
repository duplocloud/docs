---
description: A worked example — connect to an existing AWS account and run a cost optimization analysis using a HelpDesk ticket.
---

# Example: Cost Optimization

This example shows how to connect DuploCloud to an existing AWS account and immediately put the AI to work on a real operational task: identifying cost savings opportunities.

## Prerequisites

* DuploCloud is installed and running.
* You have an AWS account with existing resources.

{% stepper %}
{% step %}
## Add your AWS account as a Provider

Navigate to **AI Admin → Providers** and add your AWS account. Supply an IAM role or access credentials with read access to your AWS resources, and set the scope to the regions you want the AI to analyze.

{% hint style="info" %}
For a full guide on connecting AWS as a Provider, see [Integrating Providers](../../../getting-started/integrating-providers/README.md).
{% endhint %}
{% endstep %}

{% step %}
## Create a Workspace

Navigate to **AI Admin → Workspaces** and create a new Workspace. Attach the AWS Provider scope you just created. Assign a Persona that includes the relevant AWS skills.
{% endstep %}

{% step %}
## Open the HelpDesk and create a Ticket

Navigate to **HelpDesk** and click **New Ticket**. Select the Workspace you created. In the ticket, describe what you want:

> "Analyze our AWS account and identify the top cost savings opportunities. Include unused resources, over-provisioned instances, and any reserved instance recommendations."
{% endstep %}

{% step %}
## Review the results

The AI agent runs the analysis and returns a structured report inside the ticket — listing findings by category, estimated monthly savings, and recommended actions. You can ask follow-up questions or instruct the agent to take action directly from the ticket.
{% endstep %}
{% endstepper %}
