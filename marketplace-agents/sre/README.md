---
description: Investigate alerts and get a root-cause report.
icon: robot
---

# SRE

Turn production alerts into investigated root causes. SRE receives alerts from your monitoring tools, groups them in an alert hub, and uses an AI agent to investigate each one against your own metrics, logs, clusters, cloud accounts and code. You get a written root cause with the evidence behind it, recommended actions you can run, and optional Slack notifications.

<!-- VERIFY: the console calls this agent "SRE Workbench" (extension com.duplocloud.sre), the menu entry is "SRE" under Observability, and ClickUp calls it "AI SRE". Pick one customer-facing name for the page title and the marketplace card. -->

{% hint style="warning" %}
SRE can run commands against your infrastructure through the AI agent, and can run recommended fixes when someone chooses to run them. What it may run is controlled per hub by a command policy. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

<!-- VERIFY: admin-only versus regular user access is still to be decided by the owner (Pallavi Chaudhari, ClickUp 17twvjx4bm4). The hint above and the access tables in Permissions and Safety describe the current permission model and must be updated to the decision. -->

## What it does

1. **Collects alerts.** Each alert hub has a webhook address. Point your alert source at it and every alert becomes a record in the hub. An alert that is already firing is updated rather than duplicated, so a repeating alert does not create a repeating investigation.
2. **Triages.** On the **Alerts** tab you choose which alerts to investigate (one alert, or several related alerts together) and which to skip, with a reason. Optional **Rules** can start investigations automatically for alerts that match conditions you define.
3. **Investigates.** The AI agent reads the alert, looks for a matching runbook, runs read or diagnostic commands against the scopes you gave the hub, and writes up the result: the problem, one or more root causes, the findings that support them, the evidence (the commands it ran and their raw output), anything it could not determine, and recommended actions.
4. **Lets your team act.** Engineers can correct the root cause, run a recommended action from the **Actions** tab, split an investigation whose alerts turned out to be unrelated, and draft or create a runbook from what was learned.
5. **Notifies.** If you set up Slack, each investigation posts its progress and result to a thread.

Alert intake and de-duplication follow fixed rules. The investigation itself is done by an AI agent, so its conclusions can be wrong. Treat them as a well-evidenced starting point and check the evidence.

## Who it is for

Platform, DevOps and on-call engineers who want a first investigation done for them when an alert fires, with the evidence to check it.

## What it works with

| | |
| --- | --- |
| Alert sources | Prometheus (Alertmanager) and Grafana webhooks are read in detail. The hub form also lists Datadog, CloudWatch, PagerDuty and "Other (webhook)"; any other payload is stored as one alert with its raw content. |
| Investigation access | Scopes you attach to the hub, grouped as Observability, Kubernetes, Cloud, Infrastructure as code and Application code. |
| Runbooks | GitHub, Confluence, Google Docs, Notion or web pages. |
| Notifications | Slack |

<!-- VERIFY: the list of alert sources in the hub form is a label only. Confirm with the owner which sources are tested end to end (Prometheus and Grafana payload parsing is confirmed in code; Datadog, CloudWatch and PagerDuty are not). -->
<!-- VERIFY: free or paid. The console shows this agent as paid but it has no published version yet (open question for the owner). The repo does not state a price or plan. Do not publish a price until confirmed. -->

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need before you start, how to activate SRE from the Agent Marketplace, and how to create your first alert hub. |
| [Use](use.md) | Step-by-step walkthroughs of the main things SRE does. |
| [Permissions and Safety](permissions-and-safety.md) | What SRE can read and change, which actions need approval, and how it behaves for read-only, regular and admin users. |
| [Troubleshooting and FAQ](troubleshooting.md) | Common problems with SRE and how to fix them. |
