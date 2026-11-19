---
description: What AWS Cost Intelligence can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

## What it can read and change

AWS Cost Intelligence reads AWS with the credential of the AWS scope you registered the cost data source with.

| | What it does |
| --- | --- |
| **Reads in AWS** | Cost and usage, forecasts, commitments, recommendations, anomalies, budgets, invoices and organisation accounts. For Resource Ownership and the account scan it also reads what exists in each account (instances, volumes, snapshots, addresses, NAT gateways, VPCs, EKS, Auto Scaling, RDS, load balancers, log groups, ECR, KMS keys, Route 53 zones, S3 lifecycle settings) and CloudTrail event history (90 days). |
| **Changes in AWS** | Nothing. It never creates, changes, deletes, tags or buys anything in AWS. |
| **Changes in DuploCloud** | Its own data (cost data sources, dashboards, Action Center decisions, comments, custom dashboard versions, policies). Helpdesk tickets for Ask AI, the dashboard builder, policy rephrasing and analysis. For an organisation source, it also creates an AWS provider and scope named `finops-ci-analysis-<account>` in your workspace for each active member account, after checking the role can be assumed. |
| **Changes in Jira or ClickUp** | Only if you choose them as the ticket system. It creates tickets after you approve each one, comments on them, and closes or reopens tickets it created. It never edits their other fields or deletes them. |
| **Never** | It does not read the contents of S3 objects, secrets, parameters, log events, Lambda code or environment variables, or instance passwords. It does not store ticket bodies, prompts or credentials in its logs. |

<!-- VERIFY: "never changes AWS" is from the README, docs/ROLES.md and a search of the backend for AWS write calls. The CloudFormation templates, deployed by you, create IAM roles. Owner to confirm. -->

## Who can do what

Access follows the DuploCloud permission model. Cost data sources sit under the workspace and dashboards under each source. Two actions are granted separately by name.

| Action | Permission | What it allows |
| --- | --- | --- |
| Refresh cost data | `finops.sync`, plus edit (Put) on the source or one of its dashboards | Starts a sync now. Each sync bills Cost Explorer requests in your AWS account. A user with only read access cannot refresh even if granted `finops.sync`. |
| Export cost data | `finops.export` on the dashboard | The raw CSV and JSON export APIs (a bulk extract of per-account costs). The page's own PDF and CSV downloads need only read access. |

Neither action is marked destructive. Do not give read-only roles `finops.sync` or an action wildcard.

| User | What they can do |
| --- | --- |
| **Read-only** | Read on the workspace. View every dashboard, the Action Center lists and earlier Ask AI conversations, and download PDF and CSV from the page. Add, edit, refresh, delete, Create ticket, item decisions and comments, Settings, Ask AI and the dashboard builder are disabled with the reason shown on hover. |
| **Regular user** | Whatever their permission sets grant. With edit (Put) on dashboards: use Ask AI, work Action Center items, create tickets, change dashboard settings and build or revert custom dashboards. With Post as well: add dashboards. Add Tag Attribution, Action Center or Resource Ownership dashboards, and change what they pull, only with `finops.sync`. |
| **Administrator** | Everything, including the actions only a platform administrator can do: add, edit and delete cost data sources, delete dashboards, add, edit, switch, remove or restore policies, check accounts now, and Connect now for member accounts. An administrator also skips the per-scope check that applies to other users. |

<!-- VERIFY: rows derived from backend access attributes (SourceManagement, DashboardManagement, RefreshAccess) and docs/ROLES.md; not tested with real read-only and regular users in QA (screenshots CI-14 to CI-18). -->
<!-- VERIFY: the final role design is not decided. Today sources, policies and deletion are admin-only in code and everything else follows permission sets. The owner (Sanket Dangi) will decide whether the whole agent becomes admin-only or user-level in ClickUp DUPLOAI id 17twvjx4bkz. Rewrite this table to match. -->
<!-- VERIFY: does the platform audit log record administrator use? The code logs one event per change-making request with the user's email in the extension logs, and the Action Center records who and when per item, but the audit log was not checked. -->

A user can only use AWS, Jira or ClickUp scopes their permission sets allow. A scope attached to the workspace but denied to the user is refused, with its name. A scope from another workspace is always refused. Everything stays inside its workspace: a URL that names another workspace's source or dashboard answers 404.

## What needs approval

- **Every ticket.** Create ticket shows the exact ticket first. Nothing is created until you approve, and you are asked to review again if the item or settings change in between.
- **Every AWS command from Ask AI or a Helpdesk analysis.** Nothing runs without a person approving it in the ticket. There are no automatic approvals, and any approved rules not set by the extension are removed when the session is locked.
- **Custom dashboards.** A prompt first returns a brief. Nothing is built until you choose Build, and a build is saved as a version only when you save it. Revert asks first.
- **New policies.** A policy is reviewed against today's data before an administrator appends it.
- **Exclusions.** Excluding an item needs a reason, recorded with your name and the time.

## Safety checks

- **Read-only AWS roles.** The billing role, member read role and analysis role only read. The analysis role explicitly denies reading data and secrets even if a broader policy is attached later.
- **Command rules on AI sessions.** Before the first message the platform refuses AWS CLI calls that change anything, anything that reads a secret or mints a credential, any command that is not one plain AWS read, `--endpoint-url`, `--profile` for any scope not on the ticket, and MCP tools. Dashboard-builder and policy-rephrasing sessions refuse every command and carry no AWS credential. Workspace memory is off.
- **Ask AI allow-list.** Ask AI runs with the source's own credential, so it also refuses reads outside a list of cost and describe or list calls.
- **Measured savings.** A resolved item is confirmed against AWS's daily cost for the resource. One still costing money moves to Back in use instead of Realized.
- **Refresh limits.** Refresh needs edit rights as well as `finops.sync`, cannot start while a sync runs, and waits 15 minutes after the last request unless it failed. AI endpoints are limited to 20 calls a minute per user.
- **Safe rendering.** Ask AI answers never render images, drop raw HTML media and form tags, and keep only `https` links that open in a new tab with no referrer.
- **Credentials stay on the server.** Jira and ClickUp credentials are never sent to the browser. Mark them sensitive in AI Admin.

## Limits you should know

- Credit balances and expiry dates are not available from any AWS API.
- Some breakdowns are monthly only, so custom date ranges use whole billing months there.
- Region combines with account or service, not both (a Cost Explorer limit).
- Cost by tag is not supported on custom dashboards yet.
- Deleting a cost data source removes its cost data, dashboards and Action Center decisions. Tickets already created stay in Helpdesk, Jira or ClickUp. Uninstalling the extension keeps its data so a reinstall resumes.
- Someone with AWS tagging rights can write text that the AI later reads. Answers are rendered defensively, but approve only the AWS commands an analysis needs.

## AI data handling

- **What is sent:** to Ask AI, a snapshot of the dashboard's figures (account names, services, amounts, tag values, budget names) plus your questions. To the builder, the source's services, accounts and regions, the current dashboard definition and your earlier prompts. To a Helpdesk analysis, the item's details. To policy rephrasing, the policy text you wrote. It goes to the AI model configured for the workspace.
- **Where it is kept:** each conversation is a Helpdesk ticket, stored like any other, under **Previous conversations**. Who can read it is a platform question.
- **Credentials:** Ask AI sessions carry only the source's AWS scope. Analysis tickets carry the item's account scope. Builder and policy sessions carry none. Credentials are not placed in prompts.

<!-- VERIFY: from the extension README, docs/ROLES.md and the SECURITY-REVIEW. The review recommends a separate read-only role for Ask AI instead of the billing credential; check whether that shipped. Confirm which AI model is used and the retention of Helpdesk tickets. -->
