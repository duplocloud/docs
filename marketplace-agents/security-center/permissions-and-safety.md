---
description: What Security Center can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

## What it can read and change

| | What it does |
| --- | --- |
| **Reads** | Configuration of your AWS accounts through `describe`, `list` and `get` calls (compliance scans), findings from Security Hub, AWS Config, GuardDuty and Inspector, CloudTrail logs for impact analyses, and which CloudFormation stack or Terraform resource manages a flagged resource. |
| **Changes in AWS: account profiles** | When you apply an account security profile, it turns on the AWS services you chose (Security Hub, AWS Config, CloudTrail, GuardDuty, Inspector, the IAM password policy) and creates an event rule and queue per region, plus log storage. Needs the apply-profile permission. |
| **Changes in AWS: fixes** | Only the one AWS CLI command a fix proposed, only after someone approves it with the execute-fix permission, and only with the account's write connection. |
| **Changes in AWS: containment** | Only the containment action you select on an impact analysis, with the write connection, after a confirmation, and needing the contain permission. Each action can be undone. |
| **Changes in GitHub** | For a Terraform or CloudFormation fix it creates a new branch and opens a pull request. It pushes the branch directly to the repository when the GitHub connection allows it, and otherwise to a fork. It never merges. |
| **Changes in Jira and Slack** | Creates and updates Jira tickets and posts Slack messages, when you connect them and turn the features on. |
| **Never** | A compliance scan or impact analysis never creates, changes or deletes anything in your account. Impact analysis refuses secret values, SSM parameters, credential and token `get` calls, Lambda environment variables and code links, EC2 user data and ECS task definitions. A pull request is never merged. Templates are never deployed. |

{% hint style="warning" %}
The read-only promise applies to scans and analyses. Applying a profile, approving a CLI fix and applying a containment action change your AWS account, and each is a separate permission.
{% endhint %}

<!-- VERIFY: "pushes the branch directly to the repository when the connection allows it". The fix skill documentation says it pushes straight to the named repository and uses a fork only if that push fails. Confirm that is the shipped behaviour and wording for customers. -->
<!-- VERIFY: the extension reads Inspector, Security Hub, GuardDuty and Config findings on a schedule and from an event queue in the customer's account. Confirm the customer-facing description. -->

## How permissions work

Security Center does not ship fixed roles. It joins the platform's permission sets. Admins build permission sets from the **Security Center** branch under the workspace and assign them to groups. A set holds rules that name a resource, the verbs it allows (`GET`, `PUT`, `POST`, `DELETE`), the named actions it allows, and whether the rule covers everything under it. A user in several groups gets the union of their sets, and a refusal wins.

Seven operations are **named actions**. A verb grant never covers one, not even `ALL`. A rule must list the action or carry the wildcard `*`.

| Action | What it allows | Changes your cloud |
| --- | --- | --- |
| `security-center.propose-fix` | Open a fix (a pull request or a proposed CLI command) and answer its follow-up question. Open a scope analysis. | No |
| `security-center.execute-fix` | Approve and run a proposed AWS CLI command. | Yes |
| `security-center.grant-write` | Attach the account's write connection to a fix so it can run. | Yes |
| `security-center.apply-profile` | Apply an account security profile to the AWS account. Also needed to save frameworks, standards or the workspace override in Settings. | Yes |
| `security-center.contain` | Apply or undo a containment action on a resource in an impact analysis. | Yes |
| `security-center.create-tickets` | Create Jira tickets for selected gaps. | No |
| `security-center.run-impact-analysis` | Start an impact analysis, widen its window, or ask for more history. Each uses AI credits. | No |

Propose and execute are separate on purpose, so one person can prepare a fix and another approve and run it. Nothing in the code forces two different people: a person who holds both can do both.

Some actions are enforced as an edit (`PUT`) even though they are sent as a POST: ignore, un-ignore and close a gap, re-assess a scan, and the Slack and Jira test sends. There is no separate permission for ignoring a gap: anyone who may edit gaps may ignore them.

Every endpoint is enforced by the platform's access filter. The screens also hide or disable controls a user cannot use, with a message that says why, but that is a convenience, not the enforcement.

<!-- VERIFY: all of this comes from the extension's access declarations and README (SecurityCenterAccess.cs, the [AccessControl] attributes on each controller). The platform filter itself is not in this repo. Confirm in QA with real test users (screenshots SC-25 to SC-28). -->

## Who can do what

The extension defines what each permission allows. Which users hold which permissions is decided by the permission sets you create. The rows below describe a user whose sets match the sets suggested in the extension documentation.

| User | What they can do |
| --- | --- |
| **Read-only** | A set with `GET` on compliance scans, gaps (with everything under them, so fixes and scope analyses are readable), impact analyses and CVEs, and no actions. They can view every page, filter and export what they can see. They cannot add or re-assess a scan, ignore or close a gap, open a fix, answer a fix question, approve or run a fix, start or widen an impact analysis, contain anything, create Jira tickets, or change settings. |
| **Regular user** | Whatever their sets grant. A typical triage user adds `PUT` and `POST` on gaps (ignore, un-ignore, close, rename and refresh a fix), `PUT` on compliance scans (re-assess) and on impact analyses (narrow or reset a window, mark nodes expected), and optionally `create-tickets` and `run-impact-analysis`. A remediator adds `propose-fix`, `execute-fix` and `grant-write` on gaps, and `contain` on impact analyses. An account owner adds `GET` and `PUT` on account profiles and `apply-profile`. A settings manager adds `GET`, `PUT` and `POST` on settings. |
| **Administrator** | Administrators (the platform role) bypass every grant, named actions included, without any set being configured. Some things are administrator-only: the platform policy (AI Admin > Security Center > Settings), turning a service off in AWS from an account page, and, unless a set names it, the fix access allowlist. |

{% hint style="danger" %}
A rule with `actions: ["*"]` grants every named action under it, whatever its verbs. A set whose rules are all `GET` but also carry the action wildcard is not read-only: its users can propose and run fixes, grant write access and apply profiles. For a read-only or limited set, leave each rule's Actions field empty and add only the specific actions the set should have. Check the stored rule, not the screen.
{% endhint %}

<!-- VERIFY: the three rows. They follow the "Suggested permission sets" in the extension README and the per-endpoint access declarations; none of it has been run with real read-only, regular and admin test users. -->
<!-- VERIFY: "Administrators bypass everything" is stated in the README as confirmed on a live host. It is platform behaviour, not code in this extension. Confirm with the platform team. -->
<!-- VERIFY: Zafar's rule (2026-11-19, admin-only or approval flow). In the code: execute-fix, grant-write, apply-profile and contain are separate, destructive named actions that "ALL" never grants, and Approve and run is bound to the exact command. Not enforced: a second person approving, a confirmation dialog on Approve and run (the button sends the request directly), and an admin-only default for any of the four. Decision needed from Zafar and Darren whether to also make these admin-only by default or require a different person to approve than propose. -->

## What needs approval

- **AWS CLI fixes.** A fix is proposed first. Running it needs **Attach write access** and then **Approve and run**, each a separate permission. The page sends a fingerprint of the command on screen. If the stored command has changed since you loaded the page, the request is refused. The approved fingerprint and the approver's email are recorded, and the agent runs only a command that matches it. A command runs once.
- **Account profiles.** Applying one needs `apply-profile`. Saving frameworks, standards or the workspace override also needs it, because it re-applies every account profile and costs money.
- **Containment.** Every action and every undo asks for confirmation and lists what will change. Destructive actions are flagged. Targets that are the read or write connection's own identity are refused.
- **Pull requests.** Opening one needs `propose-fix`. You review and merge it yourself.

## Safety checks

- **Scans are read-only in code.** The collector refuses any AWS call that is not `describe`, `list`, `get`, generating the credential report, or Inspector's account status check.
- **A failed read is never a pass.** Access denied, an unsupported operation, an opted-out region or a throttle all show as **Error**, keep their weight in the score, and appear first on the Coverage tab.
- **Raw configuration stays on disk.** It is not written to the result or the ticket log.
- **One command, once, as approved.** A drafted command must be one `aws ...` invocation with no operators, redirects, substitutions or wildcards. It is checked when proposed and again before it runs. A command that does not match the approved fingerprint does not run.
- **Connections must belong to the workspace.** A new scan, fix or manual gap may only name connections attached to its own workspace.
- **The read and write connections are separate** and must be different. A fix always opens with the read-only connection.
- **Disabling is narrow.** Security Center turns off only AWS Config, GuardDuty or Inspector, only where it turned them on itself, and only when an administrator confirms. Security Hub and CloudTrail are never turned off.
- **Impact analysis is read-only** and has limits: at most 40 follow-up AWS queries and 15 minutes for the agent, a result of at most 5,000 events.
- **Scan scope is frozen.** Accounts, regions, criteria and the tag filter cannot change after create.

<!-- VERIFY: the repo has no automated test run here. Statements about the command guard come from cli_guard.py and resolve.sh. Curated commands from the fix library are not passed through the guard (they are written by DuploCloud). Confirm that is intended. -->
<!-- VERIFY: the background scan, fix and impact skills post their results as the ticket identity, which needs PUT on the resource. The README says this is "not yet confirmed for non-admin flows". Test with a non-admin user. -->
<!-- VERIFY: background workers (monitoring, account reconciler) call services directly and are assumed not to be subject to permission checks, according to the README. Confirm they cannot be triggered by a user without the matching permission. -->

## Limits you should know

- A clean result is clean against these checks. It is not SOC 2 compliance and it covers the Security criteria only. It reads AWS only, so source control rules, identity provider MFA and endpoint controls are outside it. Several areas have no check, such as Organizations service control policies, network ACLs, API Gateway, CloudFront and OpenSearch.
- Compliance history keeps counts and scores only. Findings from older runs are not kept.
- Not every failing check has an automated fix. Several can only be reported.
- Impact analysis needs a CloudTrail trail bucket it can read. There is no event-history fallback. IAM and STS calls are made in `us-east-1`, so GovCloud and China partitions are not supported.
- Deleting a user or role through containment is several calls. A failure part-way is reported as failed even though some parts were removed.
- Deleting a scan or a fix removes the record only. It does not close pull requests and does not undo a command that ran.

## AI data handling

- **What runs:** AI agents run the compliance scan, the fix proposal, scope analysis and the impact analysis review. An agent can draft a fix command or an infrastructure-as-code edit, and these are marked as drafted. Deterministic rules build the attack graph first; the agent can add to it but never remove what the rules found.
- **What stays on disk:** raw AWS configuration and collected CloudTrail files stay in the run's working directory.
- **What is published:** findings with trimmed evidence, resource identifiers and account IDs in the results. Event request and response data in an impact analysis is trimmed to 2 KB per event.
- **Geographic data:** IP location comes from a bundled offline database. There are no live threat-intelligence lookups.
- **Credentials:** each connection used by a run is made available to that ticket, and the ticket token only allows updates to its own resource.

<!-- VERIFY: which model and region the agents use, whether findings (resource names, account IDs) are sent to the model, and retention. Not in the repo. Ask Darren and the platform team. -->
