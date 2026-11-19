---
description: Step-by-step walkthroughs of the main things Security Center does.
---

# Use

## Start from the Overview

**Overview** is the home page. Its tiles show unresolved gaps, fixes awaiting approval, pull requests still open, accounts with security services on, the attack status of your newest impact analysis, your last compliance score, and CVEs due or overdue. An empty tile links to the page that fills it. A "Nothing has run yet" callout shows the two first actions once an account is connected.

<!-- VERIFY: tile names and layout against the live UI (screenshot SC-06). -->

## Run a compliance scan

1. Open **Security Center > Compliance** and select **Add**.
2. Enter a **Name** (2 to 60 characters: letters, numbers and hyphens, starting and ending with a letter or number).
3. Choose the **AWS accounts** (1 to 5) and the **Regions** (1 to 6). A resource in a region you do not list is never seen.
4. **Trust Services Criteria**: Security is always on. The other four are shown disabled.
5. Optional: a **resource tag filter** (key and value, both or neither), a **severity floor** (which findings are recorded; it does not change which checks run or the score) and **notes**.
6. Save to start the scan.

Accounts, regions, criteria and the tag filter cannot be changed after you create the scan, so the history compares like with like. For a different set, create a new scan.

<!-- VERIFY: form fields and button names (screenshots SC-07 and SC-08). The form also shows a "GRC provider" picker (Vanta or Drata). In the code its value is not sent or saved, so it is left out of these steps. -->
<!-- VERIFY: the code also has an optional Terraform repository field on the scan, a scheduled scan (Settings > Scanning) and a "full re-check interval". Confirm which are customer-facing. -->

### Read the results

The scan page has five tabs.

| Tab | What it shows |
| --- | --- |
| **Dashboard** | The posture score, severity tiles, a bar per criteria, the services with most failures, and the score history line. |
| **Findings** | One row per check per account and region. Search and filter by severity, status, criteria, control, service, account and region. Open a row for the evidence, the remediation text, a documentation link and every affected resource. |
| **Controls** | One row per SOC 2 control: Satisfied, Failing, Not evidenced in AWS or Unevaluated. Expand a row to see its checks. |
| **Coverage** | Failed and skipped reads first, then every account, region and service. Read this before trusting a high score. |
| **History** | The score over time and the checks that are new or resolved since the last run. |

The score is weighted by severity (Critical 10, High 6, Medium 3, Low 1) over the checks that ran. A check that could not read its data counts against the score, never for it. Two controls cannot be proven from configuration, so they always show as Unevaluated: recovery testing and output completeness.

<!-- VERIFY: tab names against the live UI (screenshots SC-09 to SC-12). -->
<!-- VERIFY: score history. The code keeps the last 20 runs (score and counts only) with a trend line and a new/resolved list. Darren said the trend may change. Confirm before publishing. -->

### Re-assess

Select **Re-assess** to run the same scan again on the same ticket. It adds a history entry. You cannot re-assess while a run is in progress.

History keeps counts and scores only, so it is not period-of-time audit evidence.

## Work with gaps

Gaps come from compliance scans, from continuous monitoring, and from impact analyses. Open **Gaps & Remediation** to see them all, with status and severity chips that filter the table. Open a gap to see what is wrong, the facts (account, region, resource, type, first and last seen), the controls it counts against, and what found it.

From the gap you can:

- **Get a fix** (needs the propose-fix permission).
- **Ignore, un-ignore or close** the gap (this is an edit to the gap).
- Select gaps on the list and choose **Create N Jira tickets** (needs the create-tickets permission, and a Jira connection).

<!-- VERIFY: gap statuses and the exact action labels on the gap page (screenshots SC-13 and SC-14). Closing or ignoring a gap does not touch Jira, according to the README. -->

## Get a fix

1. On a gap, select **Get a fix**. The **Plan a fix** page can also cover several gaps in one fix.
2. Choose the approach. **Let the agent find it** is the default: it asks CloudFormation which stack owns the resource, reads the Terraform state in each configured repository in order, and then fixes the resource where it is managed. Only when nothing manages it does it propose an AWS CLI command. You can also pick **Terraform**, **CloudFormation** or **AWS CLI** yourself.
3. Review the result:
   - **A pull request** against your Terraform or CloudFormation template, with the diff. Merge it and deploy through your own pipeline.
   - **A fixed template section**, when no repository holds the template. Nothing is deployed.
   - **An AWS CLI command** with an explanation. Nothing runs yet.
4. If the fix needs a value only you know (for example a destination bucket), the fix waits and asks for it. Answering needs the propose-fix permission.

Some fixes are more than a code change, such as encrypting an existing database, volume or file system. These show **This fix needs more than a code change** and an **Analyze scope** button. It starts a read-only run that reports what depends on the resource, the decisions only you can make, and a draft plan that is never run.

<!-- VERIFY: form labels (screenshots SC-15 to SC-18). Which checks have a curated Terraform or CLI fix; other checks use an agent-drafted fix, marked as drafted in the result and the pull request. -->
<!-- VERIFY: the Terraform match needs the state in a plain S3 backend with a fixed bucket and key, readable by the account's connection. Confirm this wording. -->

### Approve and run an AWS CLI fix

A CLI fix has two steps on the fix page, each its own permission:

1. **Attach write access** (grant-write permission). This attaches the account's write connection to the fix. It is only available when the account has a write connection set.
2. **Approve and run** (execute-fix permission). It runs the command once, in the AWS account shown.

Approving is approving a specific command. The page sends a fingerprint of the command on screen. If the stored command has changed since you loaded the page, the request is refused and you must reload and approve again. The approver's email and the approved fingerprint are recorded, and the agent runs nothing that does not match. A fix cannot be retried; use **Try a new fix** on the gap.

{% hint style="danger" %}
**Approve and run** changes your AWS account. Read the command and the warnings first. A drafted command is marked as drafted.
{% endhint %}

<!-- VERIFY: Approve and run has no confirmation dialog in the code (the button calls execute() directly); the protection is the separate permission and the command fingerprint. Darren: add a confirmation? -->

## Track CVEs

Open **CVEs** to see package vulnerabilities that Amazon Inspector found, each with a patch deadline. Filter by severity or deadline. Columns include the CVE (linked to the advisory), severity, resource, installed and fixed package versions, when a fix was released, first seen, due date and status.

The due date is the later of the first time Security Center saw the CVE and the date a fix was released, plus your SLA days for its severity. Set the SLAs in **Settings > General > Remediation SLAs** (defaults: critical 15, high 30, medium 90, low 180 days; or **No SLA**). Changing an SLA applies to every CVE at once.

CVEs need **continuous monitoring** on for the account, with Inspector selected. With **Send a daily CVE digest** on, one Slack message a day lists the open CVEs from your minimum severity up. It is off by default, and sends nothing on a day with nothing to fix.

<!-- VERIFY: CVE page columns and filters (screenshot SC-19). -->

## Investigate a suspected compromise (impact analysis)

1. Open **Impact analyses > New analysis** (needs the run-impact-analysis permission).
2. Choose the AWS account, enter a **name** and **description**, and set a **time window** (default the last 7 days, at most 90).
3. Add up to 25 **seeds**: an IAM user, IAM role, SSO user, or a resource (EC2 instance, Lambda function, S3 bucket, security group, EBS snapshot, AMI, KMS key or Secrets Manager secret).
4. Check the **CloudTrail** choice. The wizard lists the trails, recommends one, and verifies that it can read a log file from the trail bucket. Start needs a successful read. If the bucket is in another account, pick a **log archive connection** under **Read it with**.
5. Optionally turn on the **public endpoint check** (off by default).
6. Start the analysis. The page shows live progress.

The result has a **verdict** (Compromise confirmed, Suspicious, No evidence found or Inconclusive), a coverage strip per data source, the likely entry point, and the attack chain as a graph with a timeline. A clean quick pass says "No attack found in the selected window" and "Not yet compared against this account's history". It never says the account is clean. Use **Compare against history** and **Extend to 7 or 14 days** for a deeper look.

Other actions: **Edit window**, **Mark as expected** (hides a legitimate node and files no gap), **Export PDF**, and **Ask AI**.

### Contain

Select a node to see its containment actions. The default is **quarantine** (deactivate an access key, attach a deny-all policy to a user or role, isolate an EC2 instance in an empty security group after a snapshot, or pause a Lambda). Revoke-sessions, stop, terminate and delete are secondary. Every action and every **Undo** asks for confirmation and lists what will change. Undo restores the recorded prior state. Containment runs with the account's write connection and needs the contain permission.

<!-- VERIFY: wizard labels, verdict wording and action names (screenshots SC-20 to SC-24). -->
<!-- VERIFY: the README says that EC2 quarantine, removing ::/0 rules in IPv4-only VPCs and the exact security-group revoke request were not yet verified against a real account. Do not promise EC2 quarantine until tested. -->

## Delete

Deleting a compliance scan removes its record only. Deleting an impact analysis or a containment record is refused while a containment from it is still in effect; undo it first. Pull requests that Security Center opened stay open until you close them on GitHub.

<!-- VERIFY: where Delete appears in the UI, and whether the deletable statuses changed. -->
