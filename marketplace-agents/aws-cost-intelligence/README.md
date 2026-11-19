---
description: Shows where your AWS spend goes and where you can save.
---

# AWS Cost Intelligence

See where your AWS spend goes and what you can save, inside DuploCloud and built from your own AWS billing data. AWS Cost Intelligence reads your costs and recommendations from AWS, shows them on ready-made dashboards, turns the savings it finds into a tracked to-do list, and lets you ask questions about your spend in plain English. You do not deploy a separate AWS dashboard stack.

{% hint style="info" %}
Everything AWS Cost Intelligence does in your AWS account is read-only. It never creates, changes, deletes, tags or buys anything. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

<!-- VERIFY: "read-only in AWS" is stated in the extension README and docs/ROLES.md, and no AWS write call was found in the backend. The two CloudFormation templates only create IAM roles with read policies. Owner (Sanket Dangi) to confirm for the released version. -->

## What it does

- **Ready-made dashboards.** Add the ones you need to a cost data source:
  - **Cost and Usage**: where the money goes by service, account and region, with Compute, Storage, Database, Data Transfer, AI/ML, Analytics, Commitments, Optimisation, Idle and waste, and Resource Explorer tabs.
  - **Graviton Savings**: how much runs on Graviton, what it saves, and what could still move.
  - **KPI and Modernization**: progress against targets you set (on-demand, Spot, Graviton, gp3, commitment coverage).
  - **Extended Support**: what old RDS, EKS, OpenSearch and ElastiCache versions cost now and later.
  - **AWS Budgets**: budget against actual and forecast.
  - **Cost Anomalies**: unusual spend that AWS detected and whether it is still running.
  - **AWS Credits**: credits applied, where and how fast, checked against invoices.
  - **Tag Attribution**: who spends what by cost allocation tag, and what cannot be attributed.
  - **Resource Ownership**: who owns each resource and what was left behind after a teardown.
  - **Action Center**: every saving the other dashboards find, in one list to work through.
- **Action Center.** Resolve, exclude (with a reason) or comment on each saving. You can create a ticket for an item in Helpdesk, ClickUp or Jira. Savings are confirmed against AWS's daily cost for the resource, not just assumed.
- **Policies.** The rules the dashboards use to flag resources, such as unattached volumes or idle Elastic IPs. Administrators can add their own rules in plain language.
- **Custom dashboards.** Describe a dashboard in plain English and review a short brief before it is built. Every change is saved as a version you can revert to.
- **Ask AI.** Ask questions about the spend in a panel next to the dashboard.
- **Working with the figures.** Filters, one date range across tabs, PDF export and a light and dark theme.

<!-- VERIFY: dashboard list and tab names come from the extension README and the Add dashboard form. The README heading says "nine ready-made dashboards" but lists ten (including Action Center); confirm the count before publishing and avoid quoting a number. -->

## Who it is for

Finance, FinOps and platform teams who want one place to see AWS spend, find savings and track the work to realise them.

## What it works with

| | |
| --- | --- |
| Clouds | AWS commercial regions only. GovCloud, China and ISO regions are not supported |
| Accounts | An AWS Organization (through the management account, covering every member account) or a single standalone or member account |
| AWS services read | Cost Explorer, Cost Optimization Hub, Budgets, Invoicing, Organizations, and (for Resource Ownership and analysis) read-only calls to EC2, EKS, RDS, Auto Scaling and CloudTrail, and others listed on [Set Up](set-up.md) |
| Ticket systems | DuploCloud Helpdesk, ClickUp, Jira Cloud and Jira Data Center |
| Data | 13 months of history by default (up to 38), refreshed every 6 hours by default |
| Needs an AI model | Ask AI, custom dashboards, Policies (add a policy) and Helpdesk analysis tickets need an AI model available in your workspace. The ready-made dashboards do not |

<!-- VERIFY: free or paid. The repo does not say whether the agent itself is free or paid; the Release 1 listing and console decide this. The only cost the repo documents is the AWS bill for Cost Explorer requests (see Set Up). -->

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need before you start, the AWS and DuploCloud steps, and how to add your first cost data source. |
| [Use](use.md) | Step-by-step walkthroughs of the main things AWS Cost Intelligence does. |
| [Permissions and Safety](permissions-and-safety.md) | What AWS Cost Intelligence can read and change, which actions need approval, and how it behaves for read-only, regular and admin users. |
| [Troubleshooting and FAQ](troubleshooting.md) | Common problems with AWS Cost Intelligence and how to fix them. |
