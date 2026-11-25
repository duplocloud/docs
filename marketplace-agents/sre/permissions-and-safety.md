---
description: What SRE Workbench can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

## What it can read and change

SRE Workbench acts through an AI agent that signs in with the scopes you attach to the hub. What the agent may run there is set by the hub's [command rules](#command-rules).

| | What it does |
| --- | --- |
| **Reads** | Whatever the hub's scopes reach and its command rules allow: metrics, logs and traces, Kubernetes objects, cloud resources, and code in the repositories the source-control scopes reach. It also reads your runbooks from the runbook source you configured. |
| **Changes during an investigation** | Only what the hub's **Investigations** command rules allow. On the **Read-only** preset, that is nothing. |
| **Changes when someone runs a fix** | Whatever the recommended action's commands do, within the hub's **Remediation** scopes and command rules. This can change live infrastructure, and there is no undo. |
| **Changes in SRE Workbench** | Alert records, investigations, root causes (kept as versions), rules and runbook drafts. Deleting a hub also deletes its alerts and investigations. |
| **Changes outside your infrastructure** | Posts to Slack, if set up. Writes a runbook to your runbook source (for example by opening a pull request) only after you approve the exact destination. |
| **Never** | Creates or edits alerts other than through the ingestion endpoint. Drafts or saves a runbook unless someone asks it to. Acknowledges, silences or resolves alerts in your alert source. |

## Who can do what

DuploCloud permission sets decide what each person can do. A hub is the permission node: a grant on a hub also covers its alerts and investigations. Starting an investigation, skipping alerts and the other actions below are granted separately. Ordinary read and write access does not include them. See [Permission Sets](../../armor/access-control/permission-sets.md).

| Action | Permission | What it allows |
| --- | --- | --- |
| Ingest alerts into a hub | `sreworkbench.ingest` | Send alerts to the hub's ingestion endpoint. Grant it only to the identity your alert source uses, and nothing else to that identity. |
| Start an investigation from alerts | `sreworkbench.trigger-investigation` | Starts an agent run that runs commands under the hub's command rules and uses AI. |
| Skip alerts | `sreworkbench.skip` | Removes alerts from the triage queue, which decides what nobody looks at. |
| Manage auto-investigation rules | `sreworkbench.manage-rules` | Decides which alerts start investigations with nobody watching. |
| Execute a recommended action | `sreworkbench.execute-action` (marked destructive) | Runs commands against live infrastructure. There is no undo. Grant it only to engineers trusted to change production. |
| Edit an investigation's RCA | `sreworkbench.edit-rca` | Edit the root cause, edit it with the agent, and answer follow-up questions. This changes what the team acts on and what Slack reports. |
| Draft a runbook from an RCA | `sreworkbench.draft-runbook` | Uses AI. Nothing leaves DuploCloud. |
| Write a runbook to a repository | `sreworkbench.create-runbook` (marked destructive) | Writes outside DuploCloud with the runbook source's credentials. |
| Scan runbooks with the agent | `sreworkbench.scan-runbooks` | Starts an agent that reads your runbook source with the chosen scope's access, to fill in the hub's runbook settings. |
| Split an investigation | `sreworkbench.split` | Cannot be undone. |

| Capability | Read-only user | Regular user | Administrator |
| --- | :---: | :---: | :---: |
| See hubs, alerts, investigations, evidence and rules | Yes | Yes | Yes |
| Test rules against recent alerts | Yes | Yes | Yes |
| Create a hub or change its settings | No | If granted | Yes |
| Investigate, skip, run fixes, edit the RCA, split, or draft, write or scan runbooks | No | Each one if granted | Yes |

DuploCloud administrators bypass fine-grained permission checks.

Buttons are not hidden or greyed out for lack of permission. If you try something you are not allowed to do, the action is refused and the page says so. On an investigation the message reads: "You do not have permission to ... Ask a workspace admin to grant ..." and names the permission. The exception is **Scan runbooks**, which is greyed out with the reason when you lack **Scan runbooks with the agent**.

## What needs approval

- **Commands the hub's rules do not allow on their own.** A command that matches a block rule is refused. A command that matches no rule follows the hub's **Anything that matches no rule** setting: **Ask a person**, **Approve** or **Reject**. A command waiting for a person shows the investigation as **Needs Action**, waits in the investigation's ticket, and (with Slack) is posted to the channel. In the ticket, choose **Approve**, **Reject** or **Ignore**, then **Submit**. **Remember for this ticket** applies the same answer to every later request in that ticket, so leave it off unless you mean that.
- **Recommended actions.** Nothing runs until someone selects **Execute in Ticket** and **Run**. The run uses exactly the step that person reviewed.
- **Saving a runbook.** The agent shows the destination and how it will be delivered first, and writes only after you approve. It writes exactly the runbook you approved.
- **Automatic investigations.** Usually nobody is watching. A command that asks for approval waits until someone answers.

## Command rules

Each hub has command rules for investigations, and separate rules for fixes on **Remediation**. Choose a preset, then adjust it if you need to. The exact rules are always shown on the page.

| Preset | What the agent may run |
| --- | --- |
| **Read-only** | Inspection commands only: `kubectl get`, `describe`, `logs`, `top` and similar; `aws ... describe`, `get` and `list`; read-only shell tools such as `cat`, `grep` and `jq`; `git status`, `log`, `diff` and `show`; `curl` with GET only; and read-only Kubernetes and Grafana MCP tools. Commands that chain or redirect (with `;`, `&`, `|`, `$`, backticks, parentheses or redirects) are not allowed. Anything else is rejected. This is the default for investigations on a new hub. |
| **Custom** | Your own allow and block patterns (regular expressions) for commands and for MCP tools, plus what happens to anything that matches no rule. This is the default for fixes on a new hub, set to **Ask a person**. |
| **Full access** | Any command or MCP tool. Use it only on sandboxes. |

{% hint style="warning" %}
A hub created through the API without command rules runs on **Full access**. Hubs created in DuploCloud always get rules. Check the **Command Permissions** value on a hub's **Overview** tab.
{% endhint %}

{% hint style="warning" %}
An allow pattern matches anywhere in the command unless you anchor it. A loose pattern such as `kubectl get.*` also allows `kubectl get pods && rm -rf /`. Anchor both ends and exclude shell separators, for example `^kubectl get[^;&|$()<>]*$`. Block patterns do not need this.
{% endhint %}

Rules are fixed when an investigation is created. Changing a hub's rules affects investigations created afterwards. Only running a recommended action uses the hub's **Remediation** rules and scopes, and only if the hub has Remediation settings. Otherwise fixes run under the investigation's rules. Everything else on an investigation runs under its investigation rules: **Edit RCA with Agent**, follow-up answers, and drafting and saving runbooks.

## Safety checks

- **Repeats are recognised.** One open alert per fingerprint per hub. A repeat of a firing alert updates it and does not start another investigation. An alert that fires again after resolving is a new alert.
- **One investigation per alert.** An alert held by one investigation cannot be claimed by another.
- **Evidence is kept.** Each finding cites the command or query and its raw output, so you can check the conclusion. Findings without evidence are marked **inferred**.
- **Root cause history.** Every change is a new version, up to 20, always keeping the original, with who made it.
- **Alert, runbook and command content is treated as data.** The agent is instructed never to follow instructions found in alerts, runbooks or command output, and to report such an attempt as a finding. Keep investigation rules on **Read-only** anyway, so nothing in that content can change your systems without a person approving.
- **Size limits.** Each alert is stored up to 64 KB, and a request is limited to 500 alerts. Larger content is shortened, and the page says so.
- **Hubs are separate.** An investigation cannot span hubs, and a hub from another workspace is refused.

## Limits you should know

- An investigation is an AI run. It can be wrong or incomplete. Checks it could not conclude are listed under **Still Unknown** on the **Follow-ups** tab.
- Recommended actions and splits cannot be undone.
- The hub's scope credentials are placed in the agent's working folder while it runs, and are visible in the ticket's **Files** panel to anyone who can open the ticket. The agent can read them with any command the hub's rules allow. The **Read-only** preset allows `cat`, `jq` and similar tools, so it does not stop the agent reading those files. Attach only the scopes the hub needs, give scopes the least access that works, and limit who can open the hub's tickets.
- There is no separate audit log screen. The record is in each alert's skip reason, each action's attempts, each RCA version and each ticket.

## AI data handling

- **What the AI reads:** the alert and its details, your runbooks, the output of the commands the agent runs, and what you type in the ticket or in follow-up answers. The agent works inside a DuploCloud ticket.
- **What is stored:** alerts (including the raw payload, up to the size limit), investigations, evidence with the commands and their output, and root causes with their versions. Anyone with read access to the hub can see them.
- **What goes to Slack:** the root cause, its confidence and a link to the report; failure notices; and approval requests.
- **Which model:** the hub's **Overview** tab shows the model its investigations use. It is set by your DuploCloud AI configuration.
