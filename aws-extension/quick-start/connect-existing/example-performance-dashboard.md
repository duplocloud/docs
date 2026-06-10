---
description: >-
  Use DuploCloud to build a reusable AWS performance dashboard — pulling live
  metrics from CloudWatch across EKS, RDS, and EC2 without writing any dashboard
  code.
---

# Example: AWS Performance Dashboard

This example shows how to connect DuploCloud to an existing AWS account and use the AI agent to build a performance dashboard — covering EKS cluster health, RDS query performance, EC2 utilization, and ALB latency — all from CloudWatch data.

For full documentation on the dashboarding feature, see [AI Dashboards](../../../armor/ai-dashboards.md).

## Prerequisites

* DuploCloud is installed and running.
* An AWS Provider with read access to your account is connected. See [Integrating Providers](../../../getting-started/integrating-providers/).
* Your AWS account has CloudWatch metrics available for the resources you want to monitor.

{% stepper %}
{% step %}
### Create a Workspace with your AWS scope

Navigate to **AI Admin → Workspaces** and create a Workspace. Attach your AWS Provider scope covering the regions and resource types you want to monitor.
{% endstep %}

{% step %}
### Open Dashboard Templates

Navigate to **Observability → Dashboard Templates** and click **+ New Template**. Give the template a name — for example, "AWS Performance Overview" — and select **None / Blank** as the base. Click **Create**.
{% endstep %}

{% step %}
### Describe the dashboard to the agent

Click **Edit with Agent** on the template detail page. Select your AWS Workspace scope and click **Start Session**. In the chat, describe what you want to monitor:

> "Build an AWS performance dashboard for our production account. Include: EKS node and pod utilization, RDS query latency and connection counts, EC2 CPU and memory by instance type, and ALB request rate and 4xx/5xx error rates. Pull data from CloudWatch."

The agent queries CloudWatch, identifies the available metrics, and builds a panel structure covering each area.

{% hint style="info" %}
The agent chooses the right panel type for each metric automatically — single values for key indicators, tables for multi-resource views, and insights panels for AI-generated analysis.
{% endhint %}
{% endstep %}

{% step %}
### Review the generated template

As the agent works, the dashboard template appears in the right-hand pane. It explains each panel, which CloudWatch metric it uses, and why it was included. You can ask the agent to add, remove, or adjust panels at this stage.

Common refinements:

* "Add a panel for S3 request rates by bucket"
* "Replace the EC2 table with a single value showing total vCPUs in use"
* "Add a cost estimate panel per service"
{% endstep %}

{% step %}
### Preview with live data

Once the structure is ready, ask the agent to preview the dashboard with real CloudWatch data:

> "Run the fetch script against our production account and show me the preview."

The agent populates each panel with live values from your AWS account. Validate that the data looks correct before saving.
{% endstep %}

{% step %}
### Save and publish the template

Click **Save Dashboard Template**, then set the status to **Published**.
{% endstep %}

{% step %}
### Instantiate dashboards per environment

With the template published, create a dashboard instance for each environment — development, staging, production — by clicking **Create Dashboard** and selecting the appropriate scope each time. Each instance displays the same panel layout with data from its own AWS account or region.
{% endstep %}
{% endstepper %}

## What this covers

| AWS Service | Metrics                                                 |
| ----------- | ------------------------------------------------------- |
| EKS         | Node CPU/memory, pod restarts, cluster utilization      |
| RDS         | Query latency, active connections, IOPS, storage free   |
| EC2         | CPU utilization, network I/O, instance status           |
| ALB         | Request rate, target response time, HTTP 4xx/5xx errors |
| S3          | Request counts, error rates (optional)                  |
