---
description: What AWS Cost Intelligence can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

## What it can read and change

AWS Cost Intelligence reads AWS with the credential of the AWS scope its cost data source uses. Every AWS call it makes is a read.

| | What it does |
| --- | --- |
| **Reads in AWS** | Cost and usage, forecasts, commitments, recommendations, anomalies, budgets, invoices and the organization's accounts. With the optional member account roles, it also reads what exists in each account (for Resource Ownership and the account scan) and the last 90 days of CloudTrail. |
| **Changes in AWS** | Nothing. It never creates, changes, deletes, tags or buys anything. The CloudFormation templates you deploy create only read-only IAM roles. |
| **Changes in DuploCloud** | Its own data: cost data sources, dashboards, Action Center decisions and comments, custom dashboard versions and policies. Helpdesk tickets for Ask AI, the dashboard builder, policy drafting and analysis. For an organization source with analysis roles, an AWS provider and scope named `finops-ci-analysis-<account>` per member account, attached to the workspace. |
| **Changes in Jira or ClickUp** | Only if you choose one as the ticket system. It creates a ticket after you approve it, comments on it, and closes or reopens tickets it created. It never edits their other fields or deletes them. |
| **Never** | It doesn't read the contents of S3 objects, secrets, parameters, log events, Lambda code or environment variables. It doesn't put credentials in prompts or logs. |

## Who can do what

Access follows DuploCloud's permission sets. Cost data sources sit under the workspace, and dashboards sit under their source.

| User | Grant | What they can do |
| --- | --- | --- |
| **Viewer** | Read on the workspace | View every dashboard, the Action Center lists and earlier Ask AI conversations, and download PDF and CSV from the page. Everything else is greyed out with the reason on hover. |
| **FinOps owner** | Put on the dashboards, and Post to add dashboards | Also use Ask AI, work Action Center items, create tickets, change dashboard settings such as KPI goals, choose the ticket system, and build or revert custom dashboards. |
| **Platform administrator** | Administrator | Everything, including the actions only an administrator can do: add, edit and delete cost data sources, delete dashboards, change policies, check accounts now, and connect member accounts for analysis. |

Two rights are granted separately, by name. Neither is marked destructive, so don't give read-only roles an action wildcard.

| Right | Permission | What it allows |
| --- | --- | --- |
| Refresh cost data | `finops.sync`, plus Put on the source or one of its dashboards | Starts a sync now. Also needed to add Tag Attribution, Action Center or Resource Ownership dashboards, or to change what they pull, because each adds AWS requests to every sync. A read-only user can't refresh even with `finops.sync`. |
| Export cost data | `finops.export` on the dashboard | The raw cost-row export through the API, a bulk extract of per-account costs. The page's own PDF and CSV downloads need only Read. |

A user can only use AWS, Jira or ClickUp scopes their permission sets allow. A scope attached to the workspace but denied to the user is refused, with its name. Everything stays inside its workspace: a link to another workspace's source or dashboard answers as not found.

## What needs approval

* **Every ticket.** **Create ticket** shows the exact ticket first. Nothing is created until you approve it, and if the item or the ticket settings change in between, you're asked to review it again.
* **Every AWS command from Ask AI or a Helpdesk analysis.** Each one waits for a person to approve it in the ticket. Nothing runs automatically.
* **Custom dashboards.** A prompt first returns a brief. Nothing is built until you choose **Build**, and a build is saved only when you select **Save**. **Revert** asks first.
* **New policies.** A policy is reviewed against today's data before an administrator adds it.
* **Exclusions.** Excluding an item needs a reason, recorded with your name and the time.

## Safety checks

* **Read-only AWS roles.** The billing role, member read role and analysis role only read. The analysis role explicitly denies reading data and secrets, even if a broader policy is attached later.
* **Command rules on AI sessions.** Before the first message, the platform locks each Ask AI and analysis session so that it refuses any AWS CLI call that changes something, anything that reads a secret or creates a credential, and anything that isn't one plain AWS read, even if a person approves it. MCP tools are refused and workspace memory is off. Dashboard-builder and policy-drafting sessions carry no AWS credential and refuse every command.
* **Measured savings.** A resolved item counts as realized only when AWS's daily cost for the resource confirms it. One still costing money moves to **Back in use**.
* **Refresh limits.** A refresh can't start while a sync runs, or within 15 minutes of the last one unless it failed. The AI features are limited to 20 requests a minute per user.
* **Safe rendering.** Ask AI answers never show images, drop raw HTML media and form tags, and keep only `https` links, which open in a new tab.
* **Credentials stay on the server.** Jira and ClickUp credentials are never sent to the browser. Mark them sensitive when you register them.

## AI data handling

| AI feature | What is sent to the model | AWS credential |
| --- | --- | --- |
| Ask AI | A snapshot of the dashboard's figures (account names, services, amounts, tag values, budget names) and your questions. | The source's own scope, for reads you approve. |
| Helpdesk analysis | The Action Center item's details. | The scope for the item's account, if one is registered. |
| Custom dashboard builder | The source's services, accounts and regions, the current dashboard and your earlier prompts. | None. |
| Policy drafting | The policy text you wrote. | None. |

It all goes to the AI model configured for your workspace. Each conversation is a Helpdesk ticket, stored and access-controlled like any other.

## Limits you should know

* AWS has no API for credit balances or expiry dates.
* Some breakdowns are monthly only, so custom date ranges use whole billing months there.
* A breakdown can combine region with account or with service, not both. This is a Cost Explorer limit.
* AWS Budgets shows only the payer account's own budgets.
* Cost by tag isn't available on custom dashboards yet.
* Deleting a cost data source removes its cost data, dashboards and Action Center decisions. Tickets already created stay in Helpdesk, Jira or ClickUp. Uninstalling the extension keeps its data, so reinstalling picks up where it left off.
* Anyone with AWS tagging rights can write text that the AI later reads. Answers are rendered defensively, but approve only the AWS commands a question needs.
