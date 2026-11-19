---
description: Common problems with SRE and how to fix them.
---

# Troubleshooting and FAQ

## Common problems

| What you see | What it means | What to do |
| --- | --- | --- |
| **"The hub could not finish setting up"** after creating a hub | Provisioning of the hub failed. No webhook URL is shown. | Open **Track Provisioning Status** on the hub's Overview tab and read the ticket. Fix the cause, then save the hub again. |
| **Alerts do not arrive** | The alert source cannot reach the webhook, or its identity lacks the ingest permission. | Check the webhook URL on the Overview tab, and that the sending identity has **Ingest alerts into a hub**. Try **Ingest Alert** with a test body to confirm the hub itself works. |
| **"No alert could be read from the request body"** | The body was empty or not a JSON object. | Send a JSON object. Alertmanager and Grafana bodies with `alerts[]` create one alert per entry. |
| **The same alert does not start a new investigation** | It is still firing, so the existing record is updated instead (its occurrence count goes up). | This is expected. A new record is created after the alert resolves and fires again. |
| **An alert cannot be selected, or you get a conflict** | Another investigation already holds the alert. | Open that investigation, or wait for it to finish. |
| **Skip stays disabled** | A reason is required. | Enter a reason. |
| **"You do not have permission to ... Ask a workspace admin to grant ..."** | Your user lacks the named permission. | Ask an administrator for the permission (see [Permissions and Safety](permissions-and-safety.md)). |
| **Status shows Needs Action** | A command is waiting for approval, permissions are missing, or the run is blocked. | Open **View Ticket**. Approve or reject the command, or fix the missing access. |
| **Investigation is Failed** | The run failed. The details are in the status and in the ticket. If Slack is set up, a failure notice is posted. | Open **View Ticket**, fix the cause (for example an expired scope credential) and start a new investigation. |
| **An automatic investigation seems stuck** | A command needs approval and nobody is watching. | Approve it in the ticket, or change the hub's command rules so unattended runs do not need approval. Rules apply to new investigations only. |
| **A fix "stopped without reporting a result"** | The agent's run ended before it posted an outcome. | Check the ticket for what it did, then execute the step again if needed. |
| **"Could not prepare the fix"** | The hub's Remediation settings could not be applied to the ticket. | Check the hub's Remediation settings and try again. |
| **Runbooks card says "discovery failed"** | The runbook source was unreachable or the credential was refused. The investigation still finished, from first principles. | Check the runbook scope and location on the hub's Runbooks settings. |
| **Runbooks card says "no match" or "not configured"** | No runbook matched the alert, or no runbook source is set. | Configure a runbook source, or add a runbook for this alert. |
| **No Slack messages** | No notification scope is set on the hub, or Slack refused the message. | Set the scope in the hub's Notifications settings. Check the bot has `chat:write`, is invited to the channel, and the credential holds the bot token and channel ID. A bad Slack setup never fails the investigation. |

<!-- VERIFY: user-visible wording of the messages above (hub setup failure, conflict, fix stopped) comes from code strings; confirm in QA. Error names for Slack come from the repo's Slack setup guide. -->
<!-- VERIFY: the Alerts list may show other error text for a conflict or a refused action; confirm in QA. -->

## FAQ

**Does SRE change my infrastructure on its own?** An investigation runs the commands the hub's Investigations rules allow. Recommended fixes run only when someone selects Execute in Ticket. See [Permissions and Safety](permissions-and-safety.md).

**Can I undo a fix or a split?** No.

**How do I make sure it only reads?** Use the **Read-only** preset for Investigations and give the hub read-only scopes.

**Can several alerts share one investigation?** Yes. Select them and use **Investigate together**. If they turn out to be unrelated, **Split Investigation** divides them by root cause.

**Can I correct a wrong root cause?** Yes. Use **Edit RCA**. Earlier versions are kept.

**Which alert sources work?** Prometheus Alertmanager and Grafana payloads are read in detail. Other sources are stored as one alert with the raw payload.

**Is it free?** <!-- VERIFY: price and plan are not stated in the repo; the console shows it as paid with no published version. Confirm with the owner. -->

**Who can use it?** <!-- VERIFY: admin-only or any user is undecided (ClickUp 17twvjx4bm4). Add the answer here. -->

<!-- VERIFY: FAQ list is a first guess. Add the questions customers actually ask. -->
