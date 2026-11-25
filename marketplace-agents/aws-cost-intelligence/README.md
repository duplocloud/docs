---
description: Understand AWS spend across all your accounts.
icon: robot
---

# AWS Cost Intelligence

See where your AWS spend goes and what you can save, inside DuploCloud and built from your own AWS billing data. AWS Cost Intelligence reads your bill and recommendations from AWS, shows them on ready-made dashboards, gathers the savings it finds into one list to work through, and answers questions about your spend in plain English.

{% hint style="info" %}
AWS Cost Intelligence only reads from AWS. It never creates, changes, deletes, tags or buys anything in your accounts. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

These pages describe AWS Cost Intelligence version 0.58.18.

## What it does

1. **Ready-made dashboards.** Add the ones you need to a cost data source:
   * **Cost and Usage**: where the money goes by service, account and region, with Billing Summary, Compute, Storage, Database, Data Transfer, AI/ML, Analytics, Commitments, Optimisation, Idle and waste, and Resource Explorer tabs.
   * **Graviton Savings**: how much runs on Graviton, what it saves, and what could still move.
   * **KPI and Modernization**: progress against goals you set (on-demand share, Spot, Graviton, gp3, commitment coverage), per account.
   * **Extended Support**: what old RDS, EKS, OpenSearch and ElastiCache versions cost now and will cost later.
   * **AWS Budgets**: budget against actual and forecast, and which budgets are heading over.
   * **Cost Anomalies**: unusual spend AWS detected, whose it is, and whether it is still going.
   * **AWS Credits**: credits applied, where and how fast, checked against invoices.
   * **Tag Attribution**: who spends what by cost allocation tag, what can't be attributed and why, and tagging hygiene.
   * **Resource Ownership**: who owns each resource, priced as stacks, and what a teardown left behind.
2. **Action Center.** Every saving the other dashboards find, in one list. Resolve, exclude (with a reason) or comment on each item, or create a ticket for it in Helpdesk, Jira or ClickUp. A resolved item counts as a saving only once AWS's own daily cost for the resource confirms it.
3. **Policies.** The rules the dashboards flag resources by, such as unattached volumes or unassociated Elastic IPs. Switch each rule on or off, or add your own in plain language.
4. **Custom dashboards.** Describe a dashboard in plain English, review a short brief, then build it. Every change is saved as a version you can revert to.
5. **Ask AI.** Ask questions about the spend in a panel beside the dashboard.

## Who it is for

* **Finance and team leads** who need to see the spend and download reports.
* **FinOps owners** who find savings and track the work to realize them.
* **DuploCloud administrators** who connect AWS and decide who can do what.

## Where to find it

Under **FinOps** > **Cost Intelligence** in the left menu. Everything is per workspace: a workspace holds one or more cost data sources, and each source holds its dashboards.

## What it works with

| | |
| --- | --- |
| Clouds | AWS commercial regions. GovCloud, China and ISO regions are not supported. |
| Accounts | An AWS Organization (through its management account, covering every member account) or a single account. |
| Credential | A read-only AWS role, registered in DuploCloud as an AWS provider with a scope attached to the workspace. |
| Data | 13 months of history by default (up to 38), refreshed every 6 hours by default. |
| Ticket systems | DuploCloud Helpdesk, Jira Cloud, Jira Data Center and ClickUp. |
| AI | Ask AI, custom dashboards, adding a policy and Helpdesk analysis tickets use the AI model configured for your workspace. The ready-made dashboards don't need it. |

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need, the AWS and DuploCloud steps, adding your first cost data source and giving people access. |
| [Use](use.md) | Dashboards, the Action Center, tickets, policies, custom dashboards and Ask AI. |
| [Permissions and Safety](permissions-and-safety.md) | What the agent can read and change, what needs approval, and what viewers, FinOps owners and administrators can do. |
| [Troubleshooting and FAQ](troubleshooting.md) | Messages you might see and how to fix them. |
