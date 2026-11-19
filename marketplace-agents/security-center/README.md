---
description: Continuous cloud security and SOC 2 compliance for your AWS accounts, with gaps, fixes, CVE deadlines and attack investigation.
---

# Security Center

Security Center watches your AWS accounts for security gaps, helps you fix them, and checks your configuration against the SOC 2 Security criteria. It brings together continuous monitoring, point-in-time compliance scans, patch deadlines for vulnerabilities, and an investigation tool for suspected compromise.

{% hint style="warning" %}
Most of Security Center only reads your accounts. A few actions change your AWS accounts: applying an account security profile, running an approved AWS CLI fix, and applying a containment action. Each one is a separate permission that is never included in a general "all" grant. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

<!-- VERIFY: scope of this page. It is written from the extension's dev branch, version 0.15.30. Darren to confirm that this is what ships in the release and that every feature below is in scope for the marketplace listing. The earlier listing text describes only the compliance scan (73 checks); the code does much more. -->
<!-- VERIFY: free or paid. The Release 1 listing and console decide this; the repo does not say. -->

## What it does

| Area | What you get |
| --- | --- |
| **Compliance** | A point-in-time scan of 1 to 5 AWS accounts and 1 to 6 regions. It runs 73 read-only checks mapped to the SOC 2 Security criteria, and shows a posture score, findings, controls, a coverage table and history. |
| **Continuous monitoring** | You turn on AWS security services (Security Hub, AWS Config, CloudTrail, GuardDuty, Inspector) for an account from Settings. Findings stream in and become **gaps**. Slack alerts and Jira tickets can follow. |
| **Gaps and fixes** | Each gap is a problem with a status and severity. **Get a fix** finds how the resource is managed and proposes a pull request against your Terraform or CloudFormation, or a single AWS CLI command that waits for someone to approve and run it. |
| **CVEs** | Package vulnerabilities from Amazon Inspector, each with a patch deadline based on your SLA for its severity, and an optional daily Slack digest. |
| **Impact analysis** | When something looks compromised, it reads CloudTrail for a window of time, builds an attack graph with a verdict, and lets you contain affected resources (with undo). |
| **Overview and data flow** | A home page with tiles for gaps, fixes, patch deadlines, attack status and the last assessment, and a diagram of how your security data moves. |

Each failing compliance finding is labelled **Problem found** (a resource is misconfigured, whatever other tools you use) or **Not detected in AWS** (an AWS-native capability was not found, and another tool may cover it). A control is shown as **Failing** only when there is a problem. A clean result means clean against these checks. It does not mean your organization is SOC 2 compliant.

## Who it is for

Security, compliance and platform teams who run on AWS and want continuous visibility of gaps, a way to fix them with review, and SOC 2 evidence from AWS configuration.

## What it works with

| | |
| --- | --- |
| Cloud | AWS. The impact analysis does not support GovCloud or China partitions. |
| Criteria | Security. Availability, Confidentiality, Processing Integrity and Privacy are shown disabled. |
| Fix pull requests | Terraform (state in an S3 backend) and CloudFormation (YAML templates), through a GitHub connection |
| Integrations | Slack (alerts, CVE digest), Jira (tickets for gaps), GitHub (fix pull requests), and a GRC provider connection (such as Vanta or Drata) can be selected on a compliance scan |

<!-- VERIFY: what the GRC provider selection on the new-assessment form does. The form lists the workspace's GRC providers, but the selected value is not sent or saved anywhere in the code (see _review-notes.md). Left out of Use until Darren confirms. -->
<!-- VERIFY: menu name and agent name. The manifest names the extension "Security Center" and its agent "Compliance"; the compliance list page is titled "Compliance" in the menu. Confirm the customer-facing names. -->

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need before you start, how to activate Security Center, connect an AWS account, and the AWS permissions it needs. |
| [Use](use.md) | Step-by-step walkthroughs: run a compliance scan, work with gaps and fixes, track CVEs, and run an impact analysis. |
| [Permissions and Safety](permissions-and-safety.md) | What Security Center can read and change, the named permissions, and how it behaves for read-only, regular and admin users. |
| [Troubleshooting and FAQ](troubleshooting.md) | Common problems with Security Center and how to fix them. |
