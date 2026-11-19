---
description: Step-by-step walkthroughs of the main things Instance Scheduler does.
---

# Use

## Schedule an EC2 power action

1. Open **Scheduler > EC2** and select **Schedule Action**.
2. Under **Details**, enter a **Name** (for example `nightly-shutdown-dev`) and choose the **AWS Scope**.
3. Under **Target**, choose how to select instances:
   - **Instance IDs**: a fixed list. Instances added later are not included automatically.
   - **Tags**: filter by tag key and value pairs, then choose the matched instances.
   - **Auto Scaling Group**: see [Schedule an Auto Scaling group change](#schedule-an-auto-scaling-group-change).
   Instances that belong to an Auto Scaling group are shown but disabled in the instance list. Use the Auto Scaling Group tab for them.
4. Choose an action: **Stop**, **Start** or **Reboot**.
5. Optional: turn on the paired action ("Also schedule a Start to power back on" or "Also schedule a Stop to power off") and enter its time. Reboot has no pair.
6. Under **Schedule**, choose **One-time** (pick a date and time) or **Recurring**. For recurring, choose a frequency (hourly, daily, weekly, monthly) or enter a custom cron expression.
7. Optional: select **Dry run** to see what the schedule would affect.
8. Select **Schedule action**.

Times you enter are shown in your local timezone and converted for you. A custom cron expression is entered in UTC.

<!-- VERIFY: button and section names come from the form source (screenshots IS-05 to IS-08). Whether the paired option and "auto-tag instances" appear for every target type is inferred from the template. -->

If you are not an administrator, the button reads **Submit for Approval** and a notice says an administrator must approve the request before anything is scheduled. See [Approve a request](#approve-a-request).

## Schedule an Auto Scaling group change

1. Open **Scheduler > EC2**, select **Schedule Action**, and choose the **Auto Scaling Group** tab (or **Tags**, then show results as Auto Scaling groups).
2. Select the groups. A **CA** badge marks groups with Cluster Autoscaler enabled. Scale its Deployments to zero before setting minimum and maximum to 0.
3. Enter **Min size**, **Max size** and **Desired**.
4. Optional: turn on the restore option and enter a **Restore at** time to return capacity to the original values.
5. Choose **Execute now**, **One-time** or **Recurring**, and select **Schedule action**.

<!-- VERIFY: restore behaviour (ScheduleRestoreAction / RestoreAt) is read from field names only; confirm in the setup script that a restore schedule is actually created in AWS scope mode. -->

## Schedule an RDS stop or start

1. Open **Scheduler > RDS** and select **Schedule Action**.
2. Enter a **Schedule Name** and choose the **AWS Credential Scope**.
3. Select **Load DB Instances**, then tick the RDS instances and Aurora clusters you want. Databases already in the requested state are flagged and are skipped when the schedule runs.
4. Choose **Stop** or **Start**. For Stop, you can turn on **Take snapshot before stopping**.
5. Choose when it runs: now, a one-time date and time (UTC), or recurring.
6. Optional: for recurring schedules, add a paired Start or Stop at a second time.
7. Review the **Summary** and select **Create Schedule** (**Submit for Approval** if you are not an administrator).

{% hint style="info" %}
AWS restarts a stopped RDS instance automatically after 7 days. To keep a database stopped longer, use a recurring Stop. The form shows this warning.
{% endhint %}

When a recurring schedule falls inside a database's maintenance window, the form warns you.

<!-- VERIFY: screenshots IS-09 to IS-12. Exact wording of the maintenance-window warning. -->

## Approve a request

Administrators only.

1. Open **Scheduler > EC2** or **Scheduler > RDS**. Requests show the status **Waiting for Approval**.
2. Open the row menu (or the schedule's page) and select **Approve** or **Reject**.
3. **Approve** asks you to confirm ("This will start real provisioning against AWS") and then creates the schedule. **Reject** lets you give an optional reason that the requester sees.

A one-time request whose time has already passed cannot be approved. Ask the requester to resubmit with a new time.

A rejected request stays in the list with the status **Failed** and the rejection reason. Rejecting an edit does not restore the earlier version; edit the schedule back yourself if needed.

Deletion requests work the same way. A request to delete a live schedule shows **Pending Deletion**, and an administrator selects **Approve Deletion** or **Reject Deletion**.

<!-- VERIFY: the "Waiting for Approval" status label is from the code enum, and the request and review flow is on one page (requester and reviewer use the same list). The Slack note described request on the AI DevOps side and review on the AI Admin side; the code has no such split. Confirm with Yash. -->

## Edit, run now, pause or delete

| Task | Who | Where |
| --- | --- | --- |
| View schedules, status, execution history, logs, health | Everyone | Schedule list and detail page |
| **Edit** | Administrator applies it. Other users submit a change for approval (**Edit (request)**). | Row menu or detail page |
| **Delete** | Administrator deletes (the schedule's roles and EventBridge schedules are removed). Other users submit a request (**Delete (request)**). | Row menu or detail page |
| **Execute Now** | Administrator only | Detail page (RDS: one-time schedules; EC2: row or detail menu) |
| **Pause** and **Resume** a recurring RDS schedule | Administrator only | RDS list or detail page |
| **Delete** an RDS snapshot | Administrator only | Snapshots table on the RDS detail page |

<!-- VERIFY: whether Pause and Resume exist for EC2 schedules (the code shows them for RDS only), and where Execute Now appears on the EC2 list. -->

## Check what happened

- **Status and Exec Status** columns show whether the schedule was created and what the last run did.
- The detail page shows **Execution History**, the last executed time and, for RDS, **Snapshots**, **Health** and **Logs** (default window 24 hours, shown in your local time).
- RDS runs record the outcome as success, skipped or error.

<!-- VERIFY: EC2 logs: the page states logs are available only for DuploCloud-mode recurring schedules that use Lambda. For AWS scope mode EC2 schedules there may be no logs panel content. Check IS-13. -->
