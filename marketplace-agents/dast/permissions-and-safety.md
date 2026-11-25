---
description: What DAST can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

{% hint style="danger" %}
Only scan applications you own or have written permission to test. Full and API scans send attack payloads, can create, change or delete data, and can cause errors or load. Don't run them against production.
{% endhint %}

## What it can read and change

| | What it does |
| --- | --- |
| **Reads** | Your application over `http` or `https`: every page and endpoint it can discover within your include and exclude paths. The OpenAPI definition you give it. The application login and GitHub credentials in the scopes you choose. If you link repositories, their source code. |
| **Sends to your application** | **Baseline**: crawl requests and passive analysis, with no attack payloads. **Full**: the crawl plus active attacks against every discovered input. **API**: active attacks against the endpoints in your OpenAPI definition. If a login is set, the scan signs in and sends the session or header with its requests. |
| **Changes, only when you ask** | A scan changes nothing in your cloud accounts. Full and API scans can change data inside your application. Fix requests create a branch, commit, and open a pull request in your GitHub repository. |
| **Never** | Merges pull requests, force-pushes, or pushes to your default branch. Starts an active scan unless you chose Full or API. Turns a Baseline scan into a Full scan, or retries a Full or API scan on its own. |

### What an active scan sends

ZAP's active scan sends crafted requests, such as injection and cross-site scripting attempts, to every input it discovers. Expect errors in your application logs, alerts from a WAF or monitoring, test records in forms, and possible data changes. Use **Exclude paths** (for example `.*/logout.*`) to keep the scan away from logout and destructive endpoints.

### Where the scan runs

ZAP runs in a Docker container next to the agent, so its requests come from the agent's network address. If your application is behind a firewall or WAF, allow that address. The container is removed at the end of every scan, including failed ones.

## You're responsible for the target

DAST accepts any absolute `http` or `https` URL as a target, and doesn't check that you own the application. A Full or API scan starts as soon as someone clicks **Run scan**. The screens warn about Full scans, but the decision is yours. Make sure you have the right to test every URL you add, and limit who can run scans (see below).

## Who can do what

Access follows the DuploCloud permission model. DAST targets belong to a workspace, and their scans belong to the target. A permission set can allow or deny each action on targets and scans, and a grant on a target covers its scans.

| Action | Permission | What it allows |
| --- | --- | --- |
| View targets, scans, findings, configuration and ZAP reports | Read (GET) | Includes the ZAP report, which can contain parts of your application's responses. |
| Add a target, or run a scan | Create (POST) | **Run scan** creates a scan, which starts immediately. |
| Edit a target | Update (PUT) | Changes apply to new scans. |
| Delete a target | Delete (DELETE) | Also deletes all of its scans. |
| Raise a fix pull request | `dast.fix`, shown as **Fix DAST findings via pull request** | Lets the agent change code in the target's GitHub repositories, push a branch and open a pull request. Granted separately: the "all" permission doesn't include it. |

| User | What they can do |
| --- | --- |
| **Read-only** | View targets, scans, findings and reports. Can't add, edit or delete a target, run a scan, or raise a fix pull request. |
| **Regular user** | What their permission sets grant in the workspace: for example, run scans and edit targets, but not raise fix pull requests. |
| **Administrator** | Everything, including fix pull requests. |

## What needs approval

* **Starting a scan.** There's no approval step. Anyone with create permission can start any scan type immediately, so grant it with care.
* **Fixes.** Raising a fix pull request needs the separate `dast.fix` permission. The result is a pull request that your team reviews and merges. If the agent needs a decision, it stops and asks in the scan's chat.
* **Chat with the agent.** Commands the agent wants to run from the scan's chat follow the workspace's command approval settings.

## Safety checks

* **Passive by default.** New targets default to Baseline.
* **Settings are honored or explained.** The first lines of the ZAP log show the configuration as applied. Anything that couldn't be applied is listed in the scan's notes.
* **No silent anonymous scan.** If a target's login is unusable, the scan fails and names the missing keys, never their values.
* **Credentials stay out of results.** The login is passed to ZAP inside the container and masked in the scan log. A bearer token or header is only sent to the target's own host. Credentials aren't placed in results, chat or commits.
* **Time limit.** ZAP stops after the target's **Max duration**, plus about 10 minutes for start-up and reports.
* **Fixes stay reviewable.** One pull request per repository, on a new branch, never force-pushed. False positives aren't fixed.
* **Safe report view.** The ZAP HTML report is shown in a sandboxed frame with scripts turned off.

## Limits you should know

* DAST doesn't verify that you own the application. See [You're responsible for the target](#youre-responsible-for-the-target).
* A passive crawl can still follow links that have side effects. Use exclude paths.
* Single-page applications often expose few URLs to the crawler, so coverage can be low without a login or an API definition.
* Triage and fixes come from an AI model. Treat false-positive verdicts and generated code as suggestions to review.
* Code locations and fixes are only as good as the repositories and architecture notes you provide. If the linked code isn't the code that's running, the agent says so in the scan's notes, and its code locations are low-confidence.
* The agent can only scan what it can reach over the network.

## AI data handling

* **Sent to the workspace's AI model:** ZAP's findings (URLs, parameters, evidence snippets from responses and descriptions), the application architecture notes, the content of source files the agent opens in your linked repositories, and your questions in the scan's chat.
* **Where it's kept:** each scan has a ticket that holds its chat, stored like any HelpDesk ticket. Results are stored on the scan. ZAP's reports and log are visible on the **Artifacts** tab to anyone who can read the scan.
* **Credentials:** the login and GitHub scopes are attached to the scan's session. The agent is instructed never to print them or use the login outside the scanner.
* **Read-only re-checks:** to judge a finding, the agent may send plain `GET` or `HEAD` requests to the reported URL on the target's host, without attack payloads and without your login.
