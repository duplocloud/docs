---
description: What SRE Workbench can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

## What it can read and change

SRE acts through an AI agent that signs in with the scopes you attach to the hub. What the agent may run is set by the hub's command rules.

| | What it does |
| --- | --- |
| **Reads** | Whatever the attached scopes reach and the command rules allow: metrics, logs and traces (observability), Kubernetes objects, cloud resources, and code in the repositories the source control scopes reach. It also reads your runbooks from the runbook source you configured. |
| **Changes (only when someone runs a recommended action)** | Whatever the recommended action's commands do, within the hub's **Remediation** rules and scopes. It can change live infrastructure. There is no undo. |
| **Changes inside SRE** | Alert records, investigations, root causes (versioned), rules, and runbook drafts. Deleting a hub also deletes its alerts and investigations. |
| **Changes outside your infrastructure** | Posts to Slack if configured. Writes a runbook to your runbook source (for example opens a pull request) only after you approve the exact destination. |
| **Never** | Alerts cannot be created or edited directly; they arrive only through the webhook. An investigation does not draft or write a runbook on its own. |

<!-- VERIFY: "investigation only reads" is not guaranteed by code. During an investigation the agent can run any command the hub's Investigations rules allow. New hubs created in the UI start with the Read-only preset, but a hub with no policy (for example created through the API or before the policy existed) runs every command. Confirm the wording the owner wants. -->

## Who can do what

Access follows the DuploCloud platform permission model. The alert hub is the permission node: a grant on a hub also covers its alerts and investigations. Ordinary view, edit, create and delete permissions do not include the actions below. Each is granted separately, and the "all" permission does not include them.

| Action | Permission | What it allows |
| --- | --- | --- |
| Ingest alerts into a hub | `sreworkbench.ingest` | Send alerts to the webhook. Grant it only to the identity your alert source uses. |
| Start an investigation from alerts | `sreworkbench.trigger-investigation` | Starts an agent run that executes commands under the hub's command rules and uses AI. |
| Skip alerts | `sreworkbench.skip` | Removes alerts from the triage queue. |
| Manage auto-investigation rules | `sreworkbench.manage-rules` | Decides which alerts start investigations with nobody in the loop. |
| Execute a recommended action | `sreworkbench.execute-action` (marked destructive) | Runs commands against live infrastructure. No undo. Grant it only to engineers trusted to change production. |
| Edit an investigation's root cause | `sreworkbench.edit-rca` | Edit, send for review, or manually save the root cause. Changes what the team acts on and what Slack reports. |
| Create a runbook | `sreworkbench.create-runbook` (marked destructive) | Writes outside the platform using the hub's runbook credentials. |
| Draft a runbook | `sreworkbench.draft-runbook` | Uses AI; nothing leaves the platform. |
| Split an investigation | `sreworkbench.split` | Not reversible. |

| User | What they can do |
| --- | --- |
| **Read-only** | View hubs, alerts, investigations, evidence and rules (including the rule dry run and the command tester, which store and run nothing). Cannot create or change hubs, investigate, skip, change rules, run actions, edit the root cause, split, or draft or create runbooks. |
| **Regular user** | Whatever their permission sets grant, per hub. For example investigate and skip alerts but not run actions. |
| **Administrator** | Everything that their permission sets grant, including the named actions above. |

When a user without a permission tries an action, the investigation page shows: "You do not have permission to ... Ask a workspace admin to grant ..." naming the permission. Buttons are not hidden for lack of permission.

<!-- VERIFY: read-only and regular rows are derived from the [AccessControl] declarations and README access table; not tested with real test users (screenshots SR-18 to SR-21). -->
<!-- VERIFY: ADMIN-ONLY VERSUS USER: the owner (Pallavi Chaudhari) will decide in ClickUp 17twvjx4bm4. Rewrite this table to the decision. The repo has no administrator override or admin-only rule of its own; it relies on the platform's permission sets. Confirm whether workspace administrators bypass permission sets and whether that use is audit-logged. -->
<!-- VERIFY: upgrade note from the README: before version 0.14.0 any workspace member could use hubs, alerts and investigations. Narrow permission sets created for older installs need the new nodes and named actions granted. Confirm whether to mention this to customers. -->
<!-- VERIFY: whether buttons are disabled in the Alerts list (Investigate, Skip) for users without permission, as opposed to showing an error after the click. Only the investigation page's message was found in code. -->

## What needs approval

- **Commands the hub's rules do not pre-approve.** Each hub has command rules for investigations and separate rules for recommended fixes. A command that matches a **Block** rule is refused. A command that matches no rule follows the "anything that matches no rule" setting: **Ask a person**, **Approve** or **Reject**. A command waiting for approval appears in the investigation's ticket, shows as Needs Action, and (with Slack) pings the channel.
- **Recommended actions.** Nothing runs until someone selects **Execute in Ticket**. Fixes run under the Remediation rules. If the hub has no Remediation settings, the fix runs under the investigation's own rules.
- **Creating a runbook.** The agent shows the destination and delivery first and writes only after you approve. Pushing straight to a repository's default branch needs the runbook instructions to ask for it explicitly, plus a second confirmation.
- **Auto-investigations.** There is usually nobody to approve. A command that asks for approval waits until someone answers.

## Command rules

| Preset | What the agent may run |
| --- | --- |
| **Read-only** (default for a new hub in the UI) | Inspection commands: `kubectl get`, `describe`, `logs`, `top`, `explain`; `aws ... describe`, `get`, `list`; read-only shell tools; `git status`, `log`, `diff`, `show`; and `curl` with GET only. Commands with `;`, `&`, `|`, `$`, parentheses, redirects or backticks are not pre-approved. Mutating commands (`kubectl delete/apply/patch/exec`, `terraform apply/destroy`, `aws ... delete/terminate/stop/...`, `rm -rf`, `docker kill`) are refused. Anything else is rejected. |
| **Custom** | Your own allow and block patterns (regular expressions) for commands and for MCP tools, plus what happens to anything that matches no rule. Starts from Read-only. |
| **Full access** | Any command or MCP tool. Only for sandboxes. |

{% hint style="warning" %}
Allow patterns match any part of the command unless you anchor them, so a loose pattern such as `^kubectl get.*` also allows `kubectl get pods && rm -rf /`. Anchor both ends and exclude shell separators, for example `^kubectl get[^;&|`$()<>]*$`. Block patterns do not need this.
{% endhint %}

The policy is fixed when an investigation is created. Editing the hub applies to investigations created afterwards. The same policy also applies to Execute Action, Edit RCA with Agent, Send for Review and Create Runbook on that investigation, unless the hub has Remediation settings for fixes.

<!-- VERIFY: the extension README still says the default is Full access and describes two "Approve All / Reject All" switches. The code and hub form use a Read-only default and an "Ask a person / Approve / Reject" setting. This draft follows the code. Confirm with the owner. -->

## Safety checks

- **Alert de-duplication.** One open occurrence per alert fingerprint per hub. A repeat of a firing alert updates it; a repeat does not start a second investigation. A re-fire after the alert resolved is a new incident.
- **One investigation per alert.** An alert held by another investigation cannot be claimed again.
- **Evidence is kept.** Each finding cites the command or query and its raw result, so you can check the agent's conclusion. Findings without evidence are shown as inferences.
- **Root cause history.** Edits create versions (up to 20, always keeping the original) and record who changed it.
- **Credentials stay out of results.** The agent instructions forbid writing credentials to files, results or chat. The Slack token is read only when a message is sent and never reaches the agent.
- **Hub isolation.** An investigation cannot span hubs, and a hub from another workspace is refused.

<!-- VERIFY: the repo's production-readiness audit (version 0.11.0, 2026-11-12) lists open gaps: no prompt-injection defence for alert and runbook content, no operator-visible audit log, and no eval set. The code has since added access control. Confirm with the owner which gaps are closed in the released version before claiming any safeguard beyond those listed here. -->

## Limits you should know

- An investigation is an AI run. It can be wrong or incomplete; unconcluded checks are listed under **Unknowns**.
- Recommended actions have no undo. **Split** has no undo.
- Alert text, logs and runbook content come from outside systems and are read by the agent. Keep the Investigations command rules narrow (Read-only) so that nothing in that content can make the agent change your systems without a person approving.
- A hub's scopes are made available to the agent while it runs. Attach only the scopes the hub needs.

<!-- VERIFY: "scopes are made available to the agent" is from the README (scope credentials are placed in the agent's working directory and are visible in the ticket's Files panel). Confirm the wording and whether Files panel visibility should be stated. -->

## AI data handling

- **What is sent to the AI:** the alert payload and its details, your runbooks that match, the output of the commands the agent runs, and your instructions in chat. The agent works inside a platform ticket, like any HelpDesk ticket.
- **What is stored:** alerts (including the raw payload), investigations, evidence with raw command arguments and output, root causes and their versions. They are visible to anyone with read access to the hub.
- **What goes to Slack:** severity, title, description, summary, location and a link back to the alert source, plus the root cause, findings and recommended actions. Labels, fingerprint, receivers and the raw payload are not posted.
- **Which model:** chosen by the platform's agent configuration. The extension does not call a model itself in the default mode.

<!-- VERIFY: the model, provider, retention period and region for AI data are not in the extension code. Confirm with the owner and the platform team. -->
<!-- VERIFY: the extension README describes an "OpenSRE" mode with its own model key in the scope, but the skill file marks that mode as dormant and the hub form creates hubs in native mode. This draft describes native mode only. -->
