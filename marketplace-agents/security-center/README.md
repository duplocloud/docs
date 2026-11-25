---
description: Find security and compliance problems in your AWS accounts, get fixes prepared for your approval, track CVE deadlines and investigate suspected compromise.
icon: shield-check
---

# Security Center

Security Center finds security and compliance problems in your AWS accounts and has an AI agent prepare the fixes for you to approve. It checks your configuration against the SOC 2 Security criteria, watches your accounts for new problems, tracks patch deadlines for vulnerabilities, and helps you investigate when something looks compromised.

These pages describe Security Center version 0.15.54.

{% hint style="warning" %}
Most of Security Center only reads your AWS accounts. Three things change them: applying an account's security profile (administrators only), running an AWS CLI fix that someone approved, and containment actions. Each needs its own permission. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

## What it does

| Area | What you get |
| --- | --- |
| **Compliance scans** | A point-in-time scan of 1 to 5 AWS accounts and 1 to 6 regions against the SOC 2 Security criteria, with a posture score, findings, controls, a coverage table and history. |
| **Continuous monitoring** | Security Center turns on AWS Security Hub, AWS Config, CloudTrail, GuardDuty and Inspector in an account, and listens for their findings. New problems become **gaps**, with optional Slack alerts and Jira tickets. |
| **Gaps and fixes** | Each gap is one problem with a status and a severity. **Plan a fix** finds how the resource is managed and prepares a pull request against your Terraform or CloudFormation, or a single AWS CLI command that waits for someone to approve and run it. |
| **CVEs** | Package vulnerabilities from Amazon Inspector, each with a patch deadline based on your SLA for its severity, and an optional daily Slack digest. |
| **Impact analysis** | Starting from a stolen laptop, a leaked key or a suspicious resource, it reads CloudTrail to show what an attacker could have reached, gives a verdict, and lets you contain affected identities and resources, with undo. |
| **Overview and data flow** | A home page with your security posture at a glance, and a diagram of which accounts send what, and where it goes. |

A clean compliance result means clean against Security Center's checks. It does not mean your organization is SOC 2 compliant.

## Who it is for

- **Security and compliance teams** who want continuous visibility of gaps and SOC 2 evidence from AWS configuration.
- **Platform and DevOps engineers** who review and merge fixes, or approve AWS CLI fixes.
- **Administrators** who connect AWS accounts, assign each one to a workspace, and set the policy every workspace follows.

## Where to find it

| Where | What's there | Who uses it |
| --- | --- | --- |
| **Compliance > Security Center** in a workspace's menu | **Overview**, **Impact analyses**, **Data flow**, **Gaps & Remediation**, **CVEs**, **Plans and fixes**, **Compliance** and **Settings** | Anyone with access to the workspace's Security Center |
| **AI Admin > Security Center** | **Settings** (the policy every workspace follows) and **Cloud accounts** (which workspace owns each AWS account) | DuploCloud administrators |

Each AWS account belongs to exactly one workspace, and only that workspace can scan, fix or investigate it.

## What it works with

| | |
| --- | --- |
| Cloud | AWS. Impact analysis doesn't support the GovCloud or China partitions. |
| Criteria | SOC 2 Security (CC-series). Availability, Confidentiality, Processing Integrity and Privacy are coming. |
| Fix pull requests | Terraform (state in an S3 backend) and CloudFormation (YAML templates), through a GitHub connection |
| Integrations (optional) | GitHub for fix pull requests, Slack for alerts and the CVE digest, and Jira for a ticket per gap |
| Cost | Paid: listed in the Agent Marketplace at $1,000/month. See [Agent Marketplace and Buying Agents](../../getting-started/marketplace.md). |

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need, how to activate Security Center, assign AWS accounts to workspaces, turn on security services, and connect GitHub, Slack and Jira. |
| [Use](use.md) | Run a compliance scan, work with gaps and fixes, track CVEs, and investigate a suspected compromise. |
| [Permissions and Safety](permissions-and-safety.md) | What Security Center can read and change, the permissions that gate each action, and what read-only, regular and admin users can do. |
| [Troubleshooting and FAQ](troubleshooting.md) | Common problems and how to fix them. |
