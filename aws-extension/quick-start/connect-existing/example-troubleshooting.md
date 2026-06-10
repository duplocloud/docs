---
description: Investigate and resolve AWS infrastructure issues — EKS pod crashes, RDS degradation, ALB errors — using the AI agent as your first responder.
---

# Example: Troubleshooting and Root Cause Analysis

This example shows how to use DuploCloud to investigate issues in a live AWS environment — from an EKS pod crash to an RDS performance problem — and reach root cause faster than manual log-diving.

## Prerequisites

* DuploCloud is installed and running.
* An AWS Provider with read access to your account is connected.
* (Optional) A Kubernetes Provider is connected if you're investigating EKS workloads.

## How it works

Open a HelpDesk ticket, describe the symptom, and let the agent investigate. The agent queries CloudWatch logs, Kubernetes events, RDS performance insights, and security group rules to build a picture of what happened and why. You stay in the conversation to guide the investigation and approve any remediation steps.

---

## Scenario 1 — EKS pod crash loop

A service is restarting repeatedly. Ask the agent to investigate:

> "Our order-service pods in the production namespace keep crashing with OOMKilled. Can you investigate and tell me what's happening?"

The agent:
1. Fetches recent pod events and restart history from Kubernetes
2. Pulls CloudWatch container logs for the failed pods
3. Checks memory limits against actual usage trends
4. Reviews recent deployments for configuration changes

It returns a root cause summary — for example, a memory limit set too low for current traffic — and suggests a fix.

---

## Scenario 2 — RDS slow queries

Users are reporting slow response times. Your RDS instance is the likely culprit:

> "Our PostgreSQL RDS instance in us-east-1 has been slow for the past 2 hours. CPU is high. What's causing it?"

The agent:
1. Pulls CloudWatch metrics for CPU, IOPS, connections, and freeable memory
2. Checks RDS Performance Insights for top SQL queries by load
3. Reviews connection counts for connection pool exhaustion
4. Checks for any parameter group or maintenance window changes

It identifies the offending queries and recommends index changes or connection pool tuning.

---

## Scenario 3 — ALB returning 5xx errors

Your load balancer is returning errors for a subset of requests:

> "We're seeing a spike in ALB 5xx errors on the payments-alb load balancer over the last 30 minutes. What's going on?"

The agent:
1. Queries CloudWatch ALB access logs for 5xx patterns
2. Checks target group health and unhealthy target counts
3. Reviews security group rules for the ALB and target instances
4. Checks for recent changes to listener rules or target group settings

---

## Scenario 4 — Unexpected AWS cost spike

Your AWS bill jumped this month:

> "Our AWS costs increased by 40% last month compared to the previous month. Can you identify what changed and what's driving the increase?"

The agent:
1. Pulls Cost Explorer data broken down by service, region, and usage type
2. Identifies the top cost drivers and compares month-over-month
3. Flags any new resources created in the period
4. Highlights data transfer, NAT gateway, or Spot instance changes that commonly cause spikes

---

## Tips for effective troubleshooting tickets

{% hint style="info" %}
The more specific your symptom description, the faster the agent reaches root cause. Include: what changed recently, when the issue started, which environment or region, and any error messages you've already seen.
{% endhint %}

* **Narrow the scope** — specify the service, region, and time window
* **Share what you've already checked** — the agent will skip those paths
* **Ask for a theory first** — "What are the most likely causes?" before asking it to fix
* **Approve remediation steps explicitly** — the agent will propose fixes and wait for your go-ahead before applying anything
