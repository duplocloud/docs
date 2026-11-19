---
description: Common problems with Instance Scheduler and how to fix them.
---

# Troubleshooting and FAQ

## Common problems

| What you see | What it means | What to do |
| --- | --- | --- |
| **Status "Waiting for Approval"** | A regular user submitted a request and no administrator has approved it. Nothing exists in AWS yet. | Ask an administrator to approve or reject it (see [Use](use.md#approve-a-request)). |
| **Status "Failed" with "Rejected by administrator"** | An administrator rejected the request. | Read the reason, then submit a new request. |
| **"Only Administrators can ..."** (403) | You tried an action that only administrators can do: approve, reject, execute now, pause or resume, or delete a snapshot. | Ask an administrator. |
| **"Read-only users cannot make changes to this resource."** | Your user is read-only. | Ask for a role that can submit requests or administer schedules. |
| **"Cannot approve, the scheduled time (...) has already passed"** | A one-time request waited past its time. | Ask the requester to resubmit with a new time. |
| **"ScheduledAt ... is in the past"** | The one-time date and time is not in the future. | Pick a future time. |
| **"CronExpression ... must be a 5-field cron expression"** or **"invalid field"** | The custom cron expression is malformed. | Use five fields (minute, hour, day of month, month, day of week) with digits and `* / , -` only. Times are UTC. |
| **"Timezone ... is not a recognized IANA timezone name"** | The timezone is not valid. | Use a name such as `America/New_York`. |
| **A schedule is created but the status is "Failed"** | Creating the AWS resources failed. The most common cause is missing IAM permissions on the scope identity. | Check the provisioning ticket for the AWS error, and compare the identity with [Set Up](set-up.md#aws-permissions-for-the-scope-identity). |
| **A scope cannot be used** | The scope belongs to another workspace, or you do not have access to it. | Pick a scope attached to your workspace. |
| **A database or instance does not appear in the list** | The scope's credentials cannot see it, or the region is not covered. Instances in an Auto Scaling group are shown disabled. | Check the scope's permissions, or use the Auto Scaling Group tab. |
| **RDS run shows "skipped"** | The database was already in the requested state (for example Stop on a stopped database). | None. This is expected. |
| **Stopped RDS instance started again by itself** | AWS restarts stopped RDS instances after 7 days. | Use a recurring Stop. |
| **Schedule ran at the wrong hour** | Custom cron is in UTC, and the forms convert from your local timezone. | Check the cron preview and the timezone shown on the form. |
| **Deleted schedule still listed as "Pending Deletion"** | A regular user requested the deletion and an administrator has not approved it. | An administrator selects **Approve Deletion** or **Reject Deletion**. |

<!-- VERIFY: the messages above are copied from the backend and form source. Confirm wording in QA. The cause of "Failed" after approval is inferred from the setup script's IAM calls. -->

## If something was left behind

Deleting a schedule removes its EventBridge schedules, Lambda functions and IAM roles. If a deletion failed part way, look in the AWS account for leftovers with these name prefixes: `duplo-ec2-`, `duplo-asg-`, `rds-snap-`, `rds-paired-`, `rds-scheduler-`, `rds-paired-` and Secrets Manager secrets under `rds-snap-exec/`. RDS snapshots named `rds-sched-...` are kept (the last 7 per database) and are not removed when you delete the schedule unless an administrator deletes them.

<!-- VERIFY: snapshot behaviour on schedule deletion is inferred. Confirm what a deprovision removes, and the exact leftover resource names. -->

## FAQ

**Can a regular user schedule instances?** They can submit a request. An administrator must approve it before anything is created.

**Does it run in my account or DuploCloud's?** In your AWS account, using the scope you chose. The schedules, roles and (for RDS) Lambda functions are created there.

**Can I schedule an Auto Scaling group?** Yes, you can change its minimum, maximum and desired size on a schedule. <!-- VERIFY: see README note on ASG scope for release 1. -->

**Does stopping a database take a backup?** Only if you turn on **Take snapshot before stopping**. For recurring schedules, the snapshot is taken once when the schedule is created and later runs do not snapshot again. <!-- VERIFY: from the repo README (RDS mode 3); confirm. -->

**How many snapshots are kept?** The last 7 per database, with the prefix `rds-sched-`.

**What time zone are schedules in?** Times in the forms are your local timezone and are converted; custom cron is UTC.

<!-- VERIFY: FAQ is a first guess. Owner to add the questions customers actually ask, and whether pricing, EC2 logs and pause for EC2 belong here. -->
