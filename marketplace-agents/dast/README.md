---
description: Scan your running web apps and APIs for security flaws.
icon: robot
---

# DAST

Test a running web application or API for security weaknesses, and let the AI agent sort the results. DAST scans your application with [OWASP ZAP](https://www.zaproxy.org/), reviews every finding to set aside false positives and re-rate severity for your application, points to the file and line in your code that likely causes each issue, and can open a pull request that fixes the findings you select.

This section describes DAST version **0.1.21**.

{% hint style="warning" %}
Only scan applications you own or have written permission to test. A **Full** or **API** scan sends attack payloads to your application and can change data in it. Run those scan types only against non-production environments you own. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

## What it does

You add an application once as a **DAST target**, then run as many scans against it as you like. Each scan works in this order:

1. **Scan.** OWASP ZAP runs in a container and tests the application. ZAP's own report is available as soon as ZAP writes it.
2. **Triage.** The AI agent reviews every finding. It marks each one **Confirmed**, **False positive** or **Needs review**, and sets a severity for your application with a short reason.
3. **Map to code** (optional). If you linked the application's GitHub repositories, the agent points each finding to a file and line.
4. **Fix** (optional, on request). You select findings and the agent opens a pull request in your repository for you to review. It never merges the pull request.

Findings appear in two passes. ZAP's own ratings show first, then the triaged findings replace them.

### Scan types

| Type | What it does | Sends attack traffic? |
| --- | --- | --- |
| **Baseline (passive)** | Crawls the application and only observes its traffic. This is the default. | No |
| **Full (active)** | Crawls, then actively attacks every input it discovers. | Yes |
| **API** | Imports your OpenAPI (Swagger) definition and actively attacks the endpoints in it. | Yes |

## Who it is for

Security, platform and development teams that want a repeatable security scan of an application they own, without triaging a raw ZAP report by hand.

## Where to find it

After you activate it, DAST appears in the left menu under **Security → DAST (ZAP)**. Everything is per workspace: each workspace has its own targets and scans.

## What it works with

| | |
| --- | --- |
| Applications | Any web application or API the agent can reach over `http` or `https` |
| Scanner | OWASP ZAP, from the official `ghcr.io/zaproxy/zaproxy:stable` container image |
| API definitions | OpenAPI (Swagger), by URL |
| Application login (optional) | Form login, JSON login, bearer token or custom header, held in an **Other** provider scope |
| Source code (optional) | GitHub only |
| Fixes | Pull requests on a new branch in your GitHub repositories |
| Cloud accounts | None. DAST needs no AWS, Azure or GCP access. |

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need, how to activate DAST, connect an application login and GitHub, and add your first target. |
| [Use](use.md) | Run a scan, follow it, read the findings and reports, and fix findings with a pull request. |
| [Permissions and Safety](permissions-and-safety.md) | What DAST can read and change, what traffic each scan type sends, and what read-only, regular and admin users can do. |
| [Troubleshooting and FAQ](troubleshooting.md) | Error messages, other common problems, and answers to frequent questions. |

New to DAST? [Quick Start Step 2: Try a Marketplace Agent](../../getting-started/try-a-marketplace-agent.md) walks through a first baseline scan.
