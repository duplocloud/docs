---
description: Let developers request AWS resources directly from Slack — the agent provisions, opens a PR, and closes the Jira ticket autonomously.
---

# Example: Developer Self-Service via Slack

This example shows how developers on your team can request AWS resources — an S3 bucket, RDS instance, or SQS queue — directly from Slack, without filing a DevOps ticket or waiting for manual provisioning.

For the full generic walkthrough, see [Developer Self-Service via Slackbot](../../../../common-use-cases/developer-self-service-via-slackbot.md).

## Prerequisites

* DuploCloud is installed and running.
* An AWS Provider with write access to your account is connected.
* The DuploCloud Slackbot is installed in your Slack workspace.
* (Optional) Jira is connected as a Provider for ticket tracking.

## The scenario

A developer needs a new S3 bucket for an analytics feature. Instead of filing a DevOps request and waiting, they handle it from Slack in a few minutes.

{% stepper %}
{% step %}
## Mention the Slackbot in Slack

The developer mentions the DuploCloud Slackbot in their team channel and describes what they need:

> "@duplo-bot Create an S3 bucket for the order service analytics feature. Reference JIRA-123 for the requirements."

The bot asks for the workspace and scope, then kicks off a ticket automatically.
{% endstep %}

{% step %}
## Agent reads the Jira ticket

If a Jira ticket was referenced, the agent reads it to pull in the full requirements — bucket name, region, access policy, lifecycle rules, retention period. If anything is underspecified, the agent posts clarifying questions back into the Jira ticket and waits for answers before proceeding.

{% hint style="info" %}
No Jira? The developer can provide the requirements directly in Slack. The agent applies sensible AWS defaults for anything not specified.
{% endhint %}
{% endstep %}

{% step %}
## Agent generates Terraform and opens a PR

Once requirements are clear, the agent generates all Terraform for the S3 bucket — including the bucket, policies, lifecycle rules, and any encryption settings — and opens a pull request on GitHub. The Slackbot notifies the developer with a link to the PR.
{% endstep %}

{% step %}
## Review and merge

The developer (or a designated reviewer) reviews the pull request on GitHub. Once approved and merged, the developer tells the bot in Slack:

> "PR merged — go ahead and apply."

The agent applies the Terraform and provisions the bucket.
{% endstep %}

{% step %}
## Jira closed automatically

The developer asks the bot to update Jira:

> "Mark the ticket as done."

The bot closes the Jira ticket and adds a comment with a full summary of what was done, including the GitHub PR link and the bucket ARN.
{% endstep %}
{% endstepper %}

## AWS resources developers can request this way

Any AWS resource that can be expressed in Terraform and provisioned within your connected account:

| Resource | Example request |
|---|---|
| S3 bucket | "Create an S3 bucket for analytics logs in us-east-1 with 90-day lifecycle" |
| RDS instance | "Provision a PostgreSQL 15 RDS instance, t3.medium, in the dev environment" |
| SQS queue | "Create an SQS queue for order events with a dead-letter queue" |
| SNS topic | "Add an SNS topic for payment failure alerts" |
| IAM role | "Create an IAM role for the payments service with S3 read access" |
| ElastiCache | "Spin up a Redis ElastiCache cluster for session storage" |
