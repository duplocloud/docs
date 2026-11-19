---
description: Runs dynamic application security testing (DAST) against your running applications.
---

# DAST

Test a running web application or API for security weaknesses, then let the AI agent sort the results. DAST scans your application with OWASP ZAP, reviews every finding to remove false positives and re-rate severity for your application, points to the file and line in your code that likely causes each issue, and can open a pull request that fixes the findings you select.

{% hint style="warning" %}
A **Full** or **API** scan sends attack payloads to your application and can change data in it. Run those scan types only against non-production environments that you own. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

<!-- VERIFY: the extension is named "DAST (ZAP)" in the menu (Security > DAST (ZAP)); the stub and the docs folder say "DAST". Confirm which name customers should see. -->
<!-- VERIFY: admin-only vs user is not decided. The owner (Arun Hundaragi) decides in ClickUp 17twvjx4bm0. Rewrite the warning and the access text once decided. -->

## What it does

You register an application once as a **DAST target**, then run as many scans against it as you like. Each scan works in this order:

1. **Scan**: OWASP ZAP runs in a container and tests the application. ZAP's raw report is available as soon as it is written.
2. **Triage**: the AI agent reviews every finding. It marks each one as confirmed, false positive or needs review, and sets a severity for your application with a short reason.
3. **Map to code** (optional): if you linked your GitHub repositories, the agent points each finding to a file and line.
4. **Fix** (optional, on request): you select findings and the agent opens a pull request in your repository for you to review. It never merges the pull request.

Findings appear progressively. ZAP's own ratings show first, then the triaged findings replace them.

### Scan types

| Type | What it does | Sends attack traffic? |
| --- | --- | --- |
| **Baseline (passive)** | Crawls the application and only observes the traffic. | No |
| **Full (active)** | Crawls, then actively attacks every discovered input. | Yes |
| **API** | Imports your OpenAPI (Swagger) definition and actively attacks the endpoints in it. | Yes |

<!-- VERIFY: the screens warn about attack payloads only for Full, not for API, although API also runs ZAP's active scan (zap-plan.py). Confirm whether to add the warning in the product. -->

## Who it is for

Security, platform and development teams that want a repeatable security scan of an application they own, without triaging a raw ZAP report by hand.

## What it works with

| | |
| --- | --- |
| Applications | Any web application or API reachable over `http` or `https` from where the agent runs |
| Scanner | OWASP ZAP (official ZAP container image) |
| API definitions | OpenAPI / Swagger, by URL |
| Application login (optional) | Form login, JSON login, bearer token or custom header, held in an "other" scope |
| Source code (optional) | GitHub only |
| Fixes | Pull requests on a new branch in your GitHub repositories |

<!-- VERIFY: free or paid. The repo does not say. The Release 1 listing and console decide this. -->
<!-- VERIFY: "reachable from where the agent runs". ZAP runs in Docker on the agent host (run-scan.sh), so private or internal URLs only work if that host can reach them. Confirm where the agent host runs in the DuploCloud-managed and self-hosted cases. -->

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need before you start, how to activate DAST from the Agent Marketplace, and how to add your first application. |
| [Use](use.md) | Step-by-step walkthroughs of the main things DAST does. |
| [Permissions and Safety](permissions-and-safety.md) | What DAST can read and change, what traffic it sends, which actions need approval, and how it behaves for read-only, regular and admin users. |
| [Troubleshooting and FAQ](troubleshooting.md) | Common problems with DAST and how to fix them. |
