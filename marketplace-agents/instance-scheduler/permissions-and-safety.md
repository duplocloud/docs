---
description: What Instance Scheduler can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

## What it can read and change

Instance Scheduler acts with the AWS credential scope you pick in the form. That scope must belong to your workspace.

| | What it does |
| --- | --- |
| **Reads** | EC2 instances and their tags, Auto Scaling groups, RDS instances and Aurora clusters (including their state and maintenance window), RDS snapshots, CloudWatch logs of the schedule's Lambda functions, and the current state of scheduled instances. |
| **Changes in your AWS account** | **Stops, starts or reboots** EC2 instances. **Changes the minimum, maximum and desired size** of Auto Scaling groups. **Stops or starts** RDS instances and Aurora clusters. **Creates and deletes** RDS snapshots (a snapshot before stop, and automatic removal of old ones). **Creates** EventBridge schedules, IAM roles and, for RDS, Lambda functions and a Secrets Manager secret. Deleting a schedule removes what it created. |
| **Never** | It does not create schedules for a scope from another workspace, and it does not touch targets that are not in the schedule. Each EC2 schedule role is limited to the instances in that schedule, and each Auto Scaling role to its one group. |

<!-- VERIFY: "does not touch targets that are not in the schedule" is derived from the scoped IAM policies in the setup scripts. Tag-based schedules are resolved to a fixed list of instance IDs when saved (inferred): confirm that instances tagged later are not picked up. -->

## Who can do what

Access is decided by the user's role. The extension does not define named permission verbs of its own.

| User | What they can do |
| --- | --- |
| **Read-only** | View schedules, status, history, health and logs. Cannot create, edit, delete, request, run, pause or resume anything. The Schedule, Edit, Delete and submit buttons are greyed out with an explanatory tooltip, and the server refuses changes with "Read-only users cannot make changes to this resource." |
| **Regular user** (not an administrator, not read-only) | View everything. **Submit requests**: create a schedule, edit one, or ask to delete one. Each request waits for an administrator. Cannot approve, execute now, pause or resume, or delete snapshots. The page shows "Requires approval", and the button reads **Submit for Approval**. |
| **Administrator** | Everything: create and edit schedules that run immediately, **Execute Now**, **Pause**/**Resume**, delete snapshots, delete schedules, and **Approve**, **Reject**, **Approve Deletion** and **Reject Deletion** requests. |

<!-- VERIFY: role design is not final. At commit 4299c28 (v1.7.39) the code implements request-and-approve for regular users, but the repo README still says regular users are treated as read-only. The owner (Yash Jain) decides admin-only versus user in ClickUp 17twvjx4bm2; rewrite this table once decided. -->

<!-- VERIFY: the read-only check on the server reads a claim from the sign-in token. The README says it was not verified against a real platform token. If the claim is missing, a read-only user is treated as not read-only on the server (the greyed-out buttons still apply). A non-administrator rejection path was verified by code review only. Test with real read-only and regular users (IS-12 to IS-17). -->

{% hint style="info" %}
A schedule runner built into the platform has no signed-in user and is not blocked by these checks. It only runs schedules that already exist.
{% endhint %}

<!-- VERIFY: that note describes the background runner used by the DuploCloud-only mode. Remove it if that mode is removed from release 1. -->

## What needs approval

| Action | Administrator | Regular user |
| --- | --- | --- |
| Create a schedule | Runs immediately | Held as **Waiting for Approval**. No AWS call is made and no roles or schedules are created until an administrator approves. |
| Edit a schedule | Applies immediately | Held for approval, the same way. |
| Delete a schedule | Deletes and removes its AWS resources | Marks it **Pending Deletion**. The schedule keeps running until an administrator approves. A request that was never approved is simply deleted. |
| Execute Now, Pause, Resume, delete snapshot | Allowed | Not allowed (no approval route) |

Approval details:

- Only administrators can approve or reject, and only for something that is actually waiting.
- A one-time request whose time has passed cannot be approved.
- A rejected request is kept with the status **Failed** and the reason. A rejected edit does not roll back to the earlier version.
- Rejecting a deletion leaves the schedule running untouched.

## Safety checks

- **Validation before saving.** A one-time time in the past, a malformed cron expression (five fields, digits and `* / , -` only) and an unknown timezone are refused.
- **Scoped roles.** The roles created in your account only allow the schedule's own action on its own targets.
- **Skip, do not fail, on state mismatch (RDS).** A Stop on an already stopped database, or a Start on an available one, is recorded as skipped.
- **Snapshots (RDS).** Optional snapshot before stop; the last 7 per database are kept and older ones are deleted. Snapshot names start with `rds-sched-`.
- **Workspace boundary.** A scope from another workspace is refused.
- **Secrets.** The sign-in credential an RDS Lambda needs for its history callback is kept in AWS Secrets Manager, not in the Lambda's code or plain environment variables.
- **Deletion tears down what was created.** Deleting a schedule removes its EventBridge schedules, Lambda functions and IAM roles.

<!-- VERIFY: the repo README says the shared RDS execution role is not deleted automatically; the later code uses a per-schedule role that is deleted. Confirm current behaviour. -->

## Limits you should know

- **Stopping is not deleting.** AWS restarts a stopped RDS instance after 7 days; use a recurring Stop to keep it off.
- **Stopping an instance does not stop the cost of its disks and addresses.** <!-- VERIFY: general AWS behaviour, not stated in the repo; keep or drop. -->
- **Cron and one-time times are UTC.** The form converts times you enter in your local timezone; a custom cron expression is entered in UTC. A schedule does not follow daylight saving changes for UTC cron.

<!-- VERIFY: daylight saving statement is inferred from "cron in UTC" in the repo README; the setup script passes the display timezone to recurring EventBridge schedules, which may make times follow local time. Confirm. -->

- **ASG-managed instances** cannot be stopped individually in the instance list. Schedule the Auto Scaling group instead.
- **Cluster Autoscaler.** Scale its Deployments to zero before setting a group to 0.
- **Immediate runs** are not reversible by the product.

## AI and data handling

<!-- VERIFY: the repo does not say whether any AI model is involved. The schedules are created by a platform setup script (a provisioning job run through the platform agent) from the form's settings, but the repo does not prove whether an AI model reads or writes anything at that step, or at run time. The script treats ticket text as data and runs only the form's action. Do not describe this agent as "no AI" until the owner confirms. Confirm what data (instance and database identifiers, names, schedule settings) goes to the workspace's AI agent. -->

- The schedule's settings (names, instance and database identifiers, regions, times) are stored on the platform with the schedule.
- The platform never returns a saved DuploCloud API credential to the browser; it is redacted on reads.
