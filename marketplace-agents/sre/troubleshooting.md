---
description: Common problems with SRE Workbench and how to fix them.
---

# Troubleshooting and FAQ

## Common problems

| What you see | What it means | What to do |
| --- | --- | --- |
| **"Pick at least one Observability scope"** when creating a hub | Investigations start from metrics, logs and traces, so a hub needs an observability scope. | Go back to **Investigations** and pick one. If the list is empty, create an observability scope first. See [Integrating Providers](../../getting-started/integrating-providers/README.md). |
| **A new hub's status does not reach Complete, or it shows an error instead of "Alert hub ready"** | Setting up the hub failed. | On the hub's **Overview** tab, select **Track Provisioning Status** and read the ticket. Fix the cause, then save the hub's settings again. |
| **Alerts do not arrive** | The alert source cannot reach the ingestion endpoint, or the identity it uses lacks **Ingest alerts into a hub** on this hub. | Check the **Ingestion Endpoint** on the **Overview** tab, the token your alert source sends, and that the token's user has `sreworkbench.ingest`. Use **Ingest Alert** with a test body to confirm the hub itself works. |
| **"No alert could be read from the request body"** | The body was empty or not a JSON object. | Send a JSON object. A body with `alerts[]` records one alert per entry. |
| **A batch is refused, asking you to "Send them in smaller batches"** | One request held more than 500 alerts. | Split the batch. |
| **An alert says it "was shortened when it arrived"** | The alert was larger than 64 KB, so long fields were cut. | Nothing, usually. The full alert is still in your alert source. |
| **The same alert does not start a new investigation** | It is still firing, so the existing alert was updated and its occurrence count went up. | This is expected. A new alert is recorded once it resolves and fires again. |
| **An alert cannot be selected** | It is already being investigated, or has been. Only alerts that were never investigated, were skipped, or whose investigation failed can be selected. | Open its investigation from the alert. If that investigation mixes unrelated causes, split it instead. |
| **Skip stays disabled** | A reason is required. | Enter a reason. |
| **"You do not have permission to ... Ask a workspace admin to grant ..."** | Your user lacks the named permission. | Ask an administrator for it. See [Permissions and Safety](permissions-and-safety.md). |
| **Status shows Needs Action** | A command is waiting for approval, or the run is blocked by missing access. | Select **View Ticket**. Approve or reject the command, or fix the access. |
| **An automatic investigation seems stuck** | A command needs approval and nobody is watching. | Approve or reject it in the ticket. To avoid this, use command rules that do not ask, such as **Read-only**. New rules apply to new investigations only. |
| **Investigation is Failed** | The run failed. If Slack is set up, a failure notice was posted. | Select **View Ticket**, fix the cause (for example an expired scope credential) and start a new investigation from the alert. |
| **The runbook card says discovery failed** | The runbook source could not be reached or refused the credential, so your runbooks were never searched. The investigation still finished, without them. | Check the location and scope in the hub's **Runbooks** settings. |
| **The runbook card says no runbook matched, or none is configured** | No runbook matched the alert, or the hub has no runbook source. | Add a runbook for this alert, or set up a runbook source. You can also draft one from the investigation. |
| **Saving runbook settings fails with a format message** | A location, folder or branch is in the wrong format, for example a GitHub repository not written as `owner/repo`. | Correct the field as the message says. |
| **"Action changed"** when running a fix | Someone changed the step after you opened the page. | Reload the page, review the step again and run it. |
| **"Could not prepare the fix"** | The hub's Remediation settings could not be applied to the ticket, so the fix did not start. | Check the hub's **Remediation** settings and scopes, then try again. |
| **"The fix stopped without reporting a result"** | The agent's run ended before it reported an outcome. | Check the ticket for what it did, then run the step again if needed. |
| **No Slack messages** | No notification scope is set on the hub, or Slack refused the message. | Set the scope in the hub's **Notifications** settings. Check that the bot has `chat:write` and is in the channel, and that the credential holds the bot token and the channel ID. A Slack problem never fails an investigation. |

## FAQ

**Does SRE Workbench change my infrastructure on its own?**
An investigation runs only what the hub's **Investigations** command rules allow. On **Read-only**, that excludes anything that changes your systems. Recommended fixes run only when someone selects **Execute in Ticket** and **Run**.

**How do I make sure investigations only read?**
Keep **Investigations** on the **Read-only** preset, and attach read-only scopes.

**Can I undo a fix or a split?**
No.

**Can several alerts share one investigation?**
Yes. Select them and use **Investigate together**. If they turn out to be unrelated, **Split Investigation** divides them.

**Can I correct a wrong root cause?**
Yes. Use **Edit RCA** or **Edit RCA with Agent**. Earlier versions are kept.

**Which alert sources work?**
Any source that can send a JSON webhook with a DuploCloud API token. Prometheus Alertmanager, Grafana and CloudWatch alarm payloads are read field by field. Other payloads are stored with their title, severity and raw content.

**Which AI model does it use?**
The hub's **Overview** tab shows it. It is set by your DuploCloud AI configuration.
