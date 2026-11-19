---
description: Step-by-step walkthroughs of the main things DAST does.
---

# Use

## Run a scan

1. Open **Security > DAST (ZAP)** and select your application (a DAST target).
2. Select **Run scan**.
3. In the **Run scan** window:
   - **Scan name**: pre-filled as the target name plus the date and time. You can change it (letters, digits and hyphens, 2 to 80 characters).
   - **Scan type**: Baseline (passive), Full (active) or API. It starts on the target's default. **API** is disabled until the target has an API definition URL.
4. If you chose Full, read the warning: a full scan sends attack payloads and can change data in the application.
5. Select **Run scan**. The scan starts immediately.

<!-- VERIFY: the scan starts as soon as you select Run scan. The code has no approval step or confirmation before an active scan. Confirm this is intended and whether an ownership check or confirmation is planned (the review said active scans require proof of domain ownership). -->
<!-- VERIFY: button and field names (screenshots DA-07, DA-08). -->

## Follow progress

Open the scan from the **Scans** tab. The page shows the stages **Queued**, **Scanning**, **Triaging**, **Mapping to code** (skipped if no repositories are linked) and **Complete**. A **Needs your input** stage appears if the agent has a question while fixing.

- The **Artifacts** tab shows the live ZAP log while the scan runs, then the ZAP report (HTML and JSON) as soon as ZAP writes it.
- The **Findings** tab fills as soon as ZAP finishes, with ZAP's own ratings and a "Triaging" state. The agent then replaces them with triaged findings.
- **Ask agent** opens the scan's chat so you can ask the agent about the scan.

<!-- VERIFY: how long a scan takes. The default budget is 30 minutes and the platform limit for one scan run is 60 minutes (manifest.json), but the form accepts up to 240. Confirm real durations and what happens above 60 minutes. -->

## Read the findings

On the **Findings** tab each row has:

| Column | Meaning |
| --- | --- |
| **Severity** | Critical, High, Medium, Low or Info. Starts from ZAP's rating and is adjusted by the agent for your application, with a rationale. |
| **Finding** | The issue name. Select it for the details: URL, method, parameter, evidence, solution, references and the agent's reasons. |
| **Triage** | **Confirmed**, **False positive** or **Needs review**. |
| **Source in code** | File and line, when repositories are linked and the agent could place it. Left empty rather than guessed. |
| **Fix** | **Fix** button, when fixing is available. |

Use the triage filter and severity pills to narrow the list. The **Summary** tab shows the agent's overview and the application architecture notes it used. The **Configuration** tab shows the settings the scan ran with. If a setting could not be applied, a warning banner at the top of the scan says why.

The target page shows the latest scan, a severity bar and the scan history. Each new scan of the same target reuses the architecture notes and code locations from the previous scan, so repeat scans are faster.

## Fix findings with a pull request

This needs a linked GitHub scope and repositories on the target, and the **Fix DAST findings via pull request** permission.

1. On the **Findings** tab, select one or more findings and choose **Fix Selected Issues** (or **Fix** on one row). False positives are left out.
2. Review the list. If another finding sits in the same file, you are offered to add it to the same pull request.
3. Set the **New branch** name (default `fix/dast-<scan id>`) and, optionally, **Instructions for the agent**, such as allowed script sources for a content security policy.
4. Select **Raise fix PR**.

The agent edits the code, pushes a new branch and opens a pull request into the repository's default branch, one per repository. It never merges and never force-pushes. Find the links on the **Pull requests** tab. If a fix needs a decision from you, the scan moves to **Needs your input** and asks in the chat.

<!-- VERIFY: the review said remediation is only tested on Juice Shop. Decide how to word this limit for customers (suggested: say that fixes are a starting point to review, and that it has been tested on a small set of applications). -->
<!-- VERIFY: button names Fix Selected Issues, Raise fix PR (screenshots DA-12, DA-13). -->

## Edit or delete an application

- **Edit**: from the target page menu or the list. The name cannot be changed. Changes apply to new scans only.
- **Delete**: from the list menu. This deletes the target **and all of its scans**. Pull requests already opened stay in GitHub.

## Ask the agent

**Ask agent** on a scan opens the chat for that scan. See [Permissions and Safety](permissions-and-safety.md) for what the agent can read and send.
