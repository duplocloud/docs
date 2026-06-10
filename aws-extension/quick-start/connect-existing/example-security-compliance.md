---
description: >-
  Use DuploCloud to audit your AWS account against a compliance framework, fix
  failing controls, and track score improvements — without manually hunting down
  issues.
---

# Example: Security and Compliance

This example shows how to connect DuploCloud to an existing AWS account and run a compliance-driven remediation workflow — from fetching your current SOC 2 posture to fixing GuardDuty gaps and applying Terraform-managed logging changes.

For the full generic walkthrough, see [Security and Compliance with GRC Integration](../../../common-use-cases/security-and-compliance.md).

## Prerequisites

* DuploCloud is installed and running.
* You have an existing AWS account.
* A GRC tool (Vanta, Drata, or similar) is connected as a Provider. See [Integrating Providers](../../../getting-started/integrating-providers/).
* An AWS Provider with read/write access to your account is connected.

{% stepper %}
{% step %}
### Create a Workspace with AWS and GRC scopes

Navigate to **AI Admin → Workspaces** and create a Workspace. Attach both your AWS Provider scope and your GRC Provider scope. This gives the agent access to cross-reference your live AWS configuration against your compliance posture.
{% endstep %}

{% step %}
### Fetch your compliance status

Open the **HelpDesk** and create a new Ticket in your Workspace. Ask the agent to retrieve your current compliance status:

> "Fetch our current SOC 2 compliance status from Vanta and show me which controls are failing on AWS."

The agent connects to your GRC tool, retrieves test scores and failing control details, and categorises the issues — for example, GuardDuty not deployed in all regions, CloudTrail logging incomplete, or S3 bucket policies misconfigured.
{% endstep %}

{% step %}
### Fix AWS infrastructure issues

Ask the agent to remediate the infrastructure issues it found:

> "Fix the GuardDuty deployment gaps across all required regions."

The agent connects to your AWS account, checks GuardDuty status region by region, and enables it where missing. It then resolves any notification configuration gaps in the same pass.

{% hint style="info" %}
The agent will ask for approval before making changes. You can review each planned action before it is applied.
{% endhint %}
{% endstep %}

{% step %}
### Resolve logging issues via Terraform

For logging and configuration changes that should go through code review, ask the agent to write Terraform and open a pull request:

> "Resolve the remaining logging issues by writing Terraform. Open a pull request on GitHub and wait for approval before applying."

The agent generates all required Terraform, commits the changes to a new branch, and opens a pull request. Once you merge it, return to the ticket and tell the agent to apply.
{% endstep %}

{% step %}
### Verify score improvement

After remediation, ask the agent to re-check your GRC scores:

> "Pull the latest Vanta scores and compare against the baseline from earlier in this ticket."

The agent fetches the updated scores and shows the before/after delta — confirming the controls that have moved from failing to passing.
{% endstep %}
{% endstepper %}

## What this covers

| AWS Area   | Actions taken                                                 |
| ---------- | ------------------------------------------------------------- |
| GuardDuty  | Enabled across all required regions, notifications configured |
| CloudTrail | Logging enabled per compliance requirements                   |
| S3         | Bucket policies and logging settings corrected via Terraform  |
| GRC sync   | Compliance scores re-checked after each remediation pass      |
