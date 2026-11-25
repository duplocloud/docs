---
description: What Instance Scheduler can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

## What it can read and change

Instance Scheduler acts in AWS with the credential of the AWS scope chosen for each schedule. It can only do what that identity is allowed to do.

| | What it does |
| --- | --- |
| **Reads** | EC2 instances and their tags and state, Auto Scaling groups and their sizes, RDS instances and Aurora clusters (state, engine and maintenance window), `rds-sched-` snapshots, the schedules it created, and the logs of its RDS Lambda functions. |
| **Changes in your AWS account** | Stops, starts and reboots EC2 instances. Changes the minimum, maximum and desired size of Auto Scaling groups. Stops and starts RDS instances and Aurora clusters. Creates `rds-sched-` snapshots and deletes old ones. Creates and deletes EventBridge schedules, IAM roles and, for RDS, Lambda functions and a Secrets Manager secret (see [What it creates in your account](set-up.md#what-it-creates-in-your-account)). |
| **Changes in DuploCloud** | Stores each schedule with its targets, action, times, requester and approval decisions, and records RDS runs. |
| **Never** | Terminates, resizes or modifies instances or databases. Touches instances or databases that are not in a schedule: each role it creates allows only that schedule's action on that schedule's targets. Deletes snapshots other than its own `rds-sched-` snapshots. |

## Who can do what

Instance Scheduler uses each user's DuploCloud role. Controls a user can't use are greyed out, and the server refuses the same actions if called directly.

| Capability | Read-only user | Regular user | Administrator |
| --- | :---: | :---: | :---: |
| See schedules, their status, history, snapshots and logs | Yes | Yes | Yes |
| Create a schedule | No | Request (waits for approval) | Yes, goes live straight away |
| Edit a schedule | No | Request (**Edit (request)**) | Yes |
| Delete a schedule | No | Request (**Delete (request)**); delete their own unapproved request | Yes |
| Approve or reject requests | No | No | Yes |
| **Execute Now** | No | No | Yes |
| **Pause** and **Resume** an RDS schedule | No | No | Yes |
| Delete an RDS snapshot | No | No | Yes |

A regular user's form shows **Requires approval** and the button reads **Submit for Approval**. All users also need access to the workspace and to the AWS scope.

## What needs approval

| Action | Administrator | Regular user |
| --- | --- | --- |
| Create a schedule | Created in AWS straight away. | Saved as **Waiting for Approval**. Nothing is created in AWS until an administrator approves it. |
| Edit a schedule | Applied straight away. | Held for approval in the same way. |
| Delete a schedule | Removed from DuploCloud and AWS. | Marked **Pending Deletion**. The schedule keeps running until an administrator selects **Approve Deletion**. |

Approval rules:

- Only administrators can approve or reject, and only something that is actually waiting.
- The approve and reject prompts show who made the request. A reject reason is shown to the requester, and the list shows who rejected it.
- A one-time request whose time has passed can't be approved.
- **Reject Deletion** leaves the schedule running untouched.

## Safety checks

- **Scoped roles.** Every role Instance Scheduler creates is limited to one schedule's action on that schedule's instances, group or databases.
- **Workspace scopes only.** A schedule can only use a scope attached to its workspace. Any other scope is refused.
- **Input checks.** Names, instance and database IDs, regions, actions, cron expressions, time zones and one-time dates are checked before anything is saved. A one-time date in the past is refused.
- **State checks.** An EC2 stop or start can't be saved when every selected instance is already in that state. An RDS action skips databases already in the requested state and records them as skipped.
- **Auto Scaling group members are protected.** Instances in an Auto Scaling group can't be scheduled one by one, because the group would replace them.
- **Snapshots before stopping (RDS).** Optional, keeping the latest seven per database.
- **Clean deletion.** Deleting a schedule removes the schedules, roles, Lambda functions and secret it created in AWS.
- **Credentials are not shown.** The AWS credential is read by the platform when needed and never shown in the forms, the schedule or its logs. The DuploCloud credential an RDS Lambda function uses to record each run is kept in AWS Secrets Manager, not in the function's code or settings.

## Limits you should know

- **A stopped RDS instance starts again after 7 days.** AWS does this, and it can't be turned off. Use a recurring stop.
- **Stopping doesn't end every AWS charge.** AWS still bills a stopped instance or database for its storage, snapshots and addresses.
- **Runs that have already happened can't be undone.** To bring a resource back, start it, or run the paired or restore schedule.
- **Paired and restore schedules are separate schedules.** Edit and delete them separately.
- **Snapshots stay.** `rds-sched-` snapshots are kept when you delete a schedule, until an administrator deletes them.

## AI and data handling

Instance Scheduler builds each schedule in AWS through a provisioning ticket that DuploCloud's agent runs with the agent's own setup scripts. The ticket carries the schedule's settings: its name, the instance, group or database IDs, regions, action and times. The scripts treat those settings as data, never as instructions. Once a schedule exists, AWS runs it on time with no AI involved.

When an RDS schedule runs, its Lambda function sends the run's time, action, database, result and snapshot name back to DuploCloud for **Recent Executions**.
