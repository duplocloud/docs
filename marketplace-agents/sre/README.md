---
description: Investigate alerts and get a root-cause report.
icon: robot
---

# SRE Workbench

Turn production alerts into investigated root causes. SRE Workbench receives alerts from your monitoring tools and collects them in an alert hub. An AI agent then investigates each alert against your own metrics, logs, clusters, cloud accounts and code. You get a written root cause with the evidence behind it, recommended fixes you can run, and optional Slack notifications.

These pages describe SRE Workbench version 0.17.28.

{% hint style="warning" %}
SRE Workbench runs commands against your infrastructure through an AI agent, and runs recommended fixes when someone chooses to. Each hub's command rules decide what may run without a person approving it. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

## What it does

1. **Collects alerts.** Each alert hub has an ingestion endpoint. Point your alert source at it and every alert becomes a record in the hub. A repeat of an alert that is still firing updates the existing record, so a noisy alert does not pile up duplicates.
2. **Triages.** On the **Alerts** tab you choose which alerts to investigate (one alert, or several related alerts together) and which to skip, with a reason. **Rules** can start investigations automatically for alerts whose labels match.
3. **Investigates.** The AI agent reads the alert, checks your runbooks, runs commands against the scopes you gave the hub, and writes up the result. That is the problem, one or more root causes, the findings that support them, the evidence (each command or query and its raw output), what it could not determine, and recommended fixes.
4. **Lets your team act.** Engineers can correct the root cause, answer the agent's follow-up questions, run a recommended fix, split an investigation whose alerts turned out to be unrelated, and draft or save a runbook from what was learned.
5. **Notifies.** With Slack set up, each investigation posts its result, failures and approval requests to a channel.

Alert intake and de-duplication follow fixed rules. The investigation itself is done by an AI agent, so its conclusions can be wrong. Treat them as a well-evidenced starting point, and check the evidence.

## Who it is for

- **On-call, platform and DevOps engineers** who want a first investigation done for them when an alert fires, with the evidence to check it.
- **Administrators** who connect alert sources, choose what the agent can reach and run, and decide who can run fixes.

## Where to find it

Open **Observability > SRE** in the left menu. Each alert hub has four tabs:

| Tab | What it is |
| --- | --- |
| **Overview** | The hub's status, ingestion endpoint, model, investigation counts and settings at a glance. |
| **Alerts** | Every alert the hub has received. Investigate or skip them here. |
| **Investigations** | Every investigation, with its status and how many recommended actions have been taken. |
| **Rules** | Rules that start investigations automatically. |

Everything is per workspace.

## What it works with

| | |
| --- | --- |
| Alert sources | Any source that can send a JSON webhook. Prometheus Alertmanager, Grafana and Amazon CloudWatch alarm payloads are read field by field. Other payloads are stored with their title, severity and raw content. |
| Investigation access | Scopes you attach to the hub: Observability (required), Kubernetes, Cloud, Infrastructure as code and Application code. |
| Runbooks | GitHub, Confluence, Google Docs, Notion or web pages. |
| Notifications | Slack |
| Not covered | Paging people, acknowledging or silencing alerts in the source system, and changing alert rules. Do those in your monitoring tools. |

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need, how to activate SRE Workbench, create an alert hub and connect your alert source. |
| [Use](use.md) | Triage alerts, follow and read an investigation, correct it, run fixes, start investigations automatically and work with runbooks. |
| [Permissions and Safety](permissions-and-safety.md) | What SRE Workbench can read and change, what needs approval, command rules, and what each user can do. |
| [Troubleshooting and FAQ](troubleshooting.md) | Common problems and how to fix them. |
