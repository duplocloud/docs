---
description: What DAST can read and change, what traffic it sends, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

{% hint style="danger" %}
Only scan applications you own or have written permission to test. Full and API scans send attack payloads, can create, change or delete data, and can cause errors or load. Do not run them against production.
{% endhint %}

## What it can read and change

| | What it does |
| --- | --- |
| **Reads** | Your application over `http` or `https` (every page and endpoint it can discover within your include and exclude paths). The OpenAPI definition you give it. The application login and GitHub credentials in the scopes you choose. If you link repositories, their source code (shallow, read-only clone). |
| **Sends to your application** | Baseline: crawl requests and passive analysis, no attack payloads. Full: the crawl plus active attacks against every discovered input. API: the endpoints in your OpenAPI definition with active attacks. If a login is configured, the scan signs in and sends the session or header with its requests. |
| **Changes (only when you ask)** | The scan itself changes nothing in your cloud account. Active scans can change data inside your application. Fix requests create a new branch, commit and open a pull request in your GitHub repository. |
| **Never** | It does not merge pull requests, force-push or push to your default branch. It does not start an active scan unless you chose Full or API. It does not retry a Full or API scan on its own. It does not turn a Baseline scan into a Full scan. |

<!-- VERIFY: "does not push to the default branch" comes from the skill instructions (new branch, PR into base) and commit-push.sh. It depends on the agent following the skill; confirm whether branch protection on the repository is recommended. -->

### What traffic an active scan sends

ZAP's active scan sends crafted requests such as injection and cross-site scripting attempts to every discovered input, using two threads per host. Expect errors in your application logs, security alerts from a WAF or monitoring, test records in forms, and possible data changes. Use **Exclude paths** (for example `.*/logout.*`) to keep the scan away from logout and destructive endpoints.

### Where the scan runs, and who sees the traffic

The scan runs in a ZAP container on the agent's host, so requests come from that host's network address. Allow-list it if your application is behind a firewall or WAF. The container is removed at the end of every run.

<!-- VERIFY: the source network address customers must allow-list. The repo only says ZAP runs in Docker where the agent runs. -->

## Ownership and legal responsibility

You are responsible for having the right to test the URL you enter.

{% hint style="warning" %}
DAST does not currently check that you own the application. Any absolute `http` or `https` URL is accepted when you save a target, and a Full or API scan starts as soon as you select **Run scan**. The only protection is the warning text on the screens.
{% endhint %}

<!-- VERIFY (critical): the 2026-11-16 review said active scans require proof of domain ownership. No ownership or domain verification exists anywhere in this repo (backend validation only checks the URL scheme). Confirm where it is enforced, or that it is still to be built, and rewrite this section. Do not publish the claim "requires proof of ownership" until it is confirmed. -->
<!-- VERIFY: the warning is shown for Full only, not for API (which also runs the active scan). -->

## Who can do what

Access follows the DuploCloud platform permission model. DAST targets sit under your workspace and their scans sit under the target. A permission set can allow or deny each action on a target or scan, and a grant on a target covers its scans.

| Action | Permission | What it allows |
| --- | --- | --- |
| View targets, scans, findings, configuration and ZAP reports | Read (GET) | Includes the ZAP report, which can contain parts of your application's responses. |
| Add a target, or run a scan | Create (POST) | Run scan creates a scan, which starts immediately. |
| Edit a target | Update (PUT) | Changes apply to new scans. |
| Delete a target | Delete (DELETE) | Also deletes all of its scans. |
| Raise a fix pull request | `dast.fix` ("Fix DAST findings via pull request") | Lets the agent change code in the target's GitHub repositories, push a branch and open a pull request. Granted separately; the "all" permission does not include it. |

| User | What they can do |
| --- | --- |
| **Read-only** | View targets, scans, findings and reports. Cannot add, edit or delete a target, run a scan or raise a fix pull request. |
| **Regular user** | What their permission sets grant in the workspace: for example run scans and edit targets, but not raise fix pull requests. |
| **Administrator** | Everything, including fix pull requests. |

<!-- VERIFY: all rows are derived from the access attributes in the controllers and the platform's permission model (GET, PUT, POST, DELETE and the named action dast.fix). Nothing here was tested with real test users. Confirm in QA with a read-only, a regular and an admin user (screenshots DA-14 to DA-17). -->
<!-- VERIFY: role design is not final. The owner (Arun Hundaragi) decides admin-only vs user in ClickUp 17twvjx4bm0. Given that active scans can change data and fixes write to code, it may be admin-only. Rewrite this table to the shipped behaviour. -->
<!-- VERIFY: the extension screens do not hide or disable buttons by permission (only by configuration, for example Fix needs linked repositories and API needs a definition URL). Confirm whether the platform disables Run scan, Edit, Delete and Fix for read-only users, and with what message. -->
<!-- VERIFY: administrator override and audit logging are platform behaviour; the repo does not describe them. Confirm and, if true, add "each use is recorded in the audit log". -->
<!-- VERIFY: dast.fix is not marked as destructive in the code, although it writes to your repositories. Confirm whether it should be. -->

## What needs approval

- **Starting a scan.** There is no approval step. A user with create permission can start any scan type immediately. Grant it with care.
- **Fixes.** Raising a fix pull request needs the separate `dast.fix` permission. The result is a pull request that your team reviews and merges; nothing is merged for you. If the agent needs a product decision, it stops and asks in the scan's chat.
- **Chat with the agent.** Commands the agent wants to run follow the workspace's command approval settings.

<!-- VERIFY: confirm that command approval in the scan chat applies as in other agents, and what the agent is allowed to run there. -->

## Safety checks

- **Passive by default.** New targets default to Baseline. The agent never upgrades the scan type on its own, and never reruns a Full or API scan unless you ask.
- **Settings are honoured or explained.** The scan's first log lines show the configuration as applied. Anything that could not be applied is listed as a warning.
- **No silent anonymous scan.** If a login scope is selected but unusable, the scan fails and names the missing keys (never the values).
- **Credentials stay out of results.** Logins are passed to ZAP inside the container and masked in the scan log. A bearer or header credential is only sent to the target's own address, never to other hosts. Credentials are not placed in results, chat or commits.
- **Time limit.** A scan is capped by its Max duration plus about 10 minutes for start-up and reports.
- **Container cleanup.** The ZAP container is removed after every run, including failures.
- **Fixes stay reviewable.** One pull request per repository, on a new branch (suffixed if it exists), committed as "DuploCloud AI Helpdesk", never force-pushed. Findings marked false positive are not fixed.
- **Report view.** The HTML ZAP report is shown in a sandboxed frame without scripts.

## Limits you should know

- There is **no ownership verification** (see above).
- A passive crawl can still follow links that have side effects. Use exclude paths.
- Single-page applications often expose few URLs to the crawler, so coverage can be low without a login or an API definition.
- Triage and fixes are made by an AI model. Treat false-positive verdicts and generated code as suggestions to review.
- The agent is told never to dismiss a ZAP High finding without evidence, but you should still review dismissed findings.
- Code locations and fixes are only as good as the repository and architecture notes provided. Fix quality has so far been tested on a deliberately vulnerable demo application only.
- Targets that are not reachable from the agent's host cannot be scanned.

<!-- VERIFY: the "tested only on Juice Shop" limit comes from the 2026-11-16 review, not from the repo. The repo has no automated tests for the extension. -->

## AI data handling

- **What is sent to the AI model:** ZAP's findings (URLs, parameters, evidence snippets from responses, descriptions), the application architecture notes, and the content of source files the agent opens in your linked repositories, plus your questions in the scan chat. The agent reads at most about 15 files to build the architecture notes, then the files it needs to place or fix findings.
- **Where it is kept:** each scan has a platform ticket (the chat) stored like any HelpDesk ticket. Results are stored on the scan. ZAP reports and logs are kept in the scan's working directory and visible on the **Artifacts** tab to anyone who can read the scan.
- **Credentials:** the login and GitHub scopes are attached to the scan session. The agent's instructions forbid printing them or using the login outside the scanner, and files holding them are wiped after each turn.
- **Read-only re-checks:** to judge a finding, the agent may send plain `GET` or `HEAD` requests to the reported URL on the target's host, without attack payloads and without your login.

<!-- VERIFY: which model and region the workspace's AI agent uses, and the data retention of tickets. Confirm with the platform team. -->
<!-- VERIFY: all text here is derived from the skill instructions (provision-dast-scan) and scripts. The instructions are followed by an AI agent, not enforced by code, except for the scanner behaviour in run-scan.sh and zap-plan.py. -->
