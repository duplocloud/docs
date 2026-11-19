---
description: Step-by-step walkthroughs of the main things SRE does.
---

# Use

Open **Observability > SRE**. Each alert hub has four tabs: **Overview**, **Alerts**, **Investigations** and **Rules**.

## Triage and investigate alerts

1. Open the **Alerts** tab. Filter by investigation status, severity, or state (firing or resolved).
2. Select one or more alerts.
3. To investigate, select **Investigate alert**, or **Investigate together** when you selected several related alerts. They share one investigation.
4. To skip alerts, enter a **Reason** and select **Skip**. A reason is required, so the decision can be reviewed later.

Alerts that are already being investigated cannot be selected again. If another investigation already holds an alert, you are told so and nothing changes.

<!-- VERIFY: exact button wording ("Investigate alert" / "Investigate together", "Skip") from the UI source; screenshots SR-08 to SR-10. -->

## Send an alert by hand

On the **Alerts** tab select **Ingest Alert**, paste an Alertmanager or Grafana style JSON body and select **Ingest**. This is the same call your alert source makes. If a hub rule matches, an investigation starts immediately.

Sending the same alert again while it is still firing updates the existing record and increases its occurrence count. It does not create a duplicate and does not run the rules again. If the alert resolved and then fires again, that is a new incident and a new record.

## Start investigations automatically

1. Open the **Rules** tab and select **Add the first rule**.
2. Name the rule and add one or more conditions on the alert's labels (for example `severity` equals `critical`). All conditions must match. Rules are checked in order and the first match wins.
3. Use **Dry run** to see which of the hub's recent alerts would match. It changes nothing.
4. Save the rules.

Only newly created alerts are matched. An investigation started by a rule is marked as automatic and records which rule started it.

{% hint style="warning" %}
An automatic investigation usually has nobody watching it. If the hub's command rules ask a person to approve a command, the run waits for that approval. Choose command rules that fit unattended runs. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

## Follow an investigation

Open an investigation from the **Investigations** tab (or from its alert). While it runs, the **RCA** tab shows an execution pipeline with the current phase: Initializing, Reading alert, Checking runbooks, Investigating, Generating RCA and Notifying. A status shows Processing, Needs Action, Failed, Pending Remediation or Complete. **View Ticket** opens the agent's conversation, where you can approve commands that need approval.

<!-- VERIFY: phase names are taken from the agent instructions; confirm they appear this way in the UI (screenshot SR-11). Confirm the typical duration of an investigation, which the repo does not state. -->

## Read the result

When it completes, the **RCA** tab shows:

- the **problem** statement,
- one or more **root causes**, each with the alerts it explains,
- **findings** that support each cause, each citing the **evidence**: the command or query that was run and its raw output,
- a **Runbooks** card saying whether runbooks were used, none matched, none are configured, or the runbook source could not be reached.

Other tabs: **Unknowns** (checks that could not be concluded, with the reason), **Actions** (recommended fixes) and **Runbook**.

## Correct the root cause

Select **Edit RCA** on the Root Cause or Findings card to edit the problem, root causes, findings and recommended actions directly, then **Save RCA**. Or choose **Edit RCA with Agent** from the menu to correct it in a conversation with the agent. The original is kept: previous versions are listed on the RCA tab and record who changed it.

## Run a recommended action

1. Open the **Actions** tab and expand a step to see its commands.
2. Select **Execute in Ticket**. If an attempt failed, the button reads **Retry Execution in Ticket**.
3. Follow the run in the ticket. Commands that the hub's remediation rules do not pre-approve wait for a person to approve them there.

**Details** shows what was done and every command that ran with its result. Each attempt is kept.

{% hint style="warning" %}
Executing an action can change live infrastructure and cannot be undone. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

## Split an investigation

If an investigation covers alerts that turned out to be unrelated causes, use **Split Investigation**. A preview shows what moves to the new investigation and what stays. Splitting cannot be reversed.

## Draft or create a runbook

From the header menu or the **Runbook** tab, select **Draft Runbook** to have the agent write a draft from what the investigation established. Nothing is saved to your runbook source. Select **Create Runbook** to have the agent save it where your runbooks live. It shows you the exact destination and how it will be delivered (for example a pull request), and writes only after you approve.

## Notifications

If you set a Slack scope on the hub, each investigation opens one Slack thread when it starts. Replies follow with the root cause, findings and recommended actions, a notice if the run fails, and a ping when a command is waiting for approval. A failed or missing Slack message never fails the investigation.
