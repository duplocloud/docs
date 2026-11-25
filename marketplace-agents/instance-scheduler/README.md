---
description: Stop and start EC2 and RDS on a schedule, and stop paying for idle resources.
icon: robot
---

# Instance Scheduler

Switch AWS compute and databases off when nobody needs them, and back on when they do. Instance Scheduler stops, starts and reboots EC2 instances, changes the size of EC2 Auto Scaling groups, and stops and starts RDS instances and Aurora clusters. It runs each action now, once at a set time, or on a recurring schedule, and builds the schedules in your own AWS account.

{% hint style="warning" %}
Instance Scheduler stops, starts and reboots real instances and databases in your AWS account. Administrators' schedules go live as soon as they are saved. Schedules from other users wait until an administrator approves them. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

These pages describe Instance Scheduler version 1.7.68.

## What it does

**EC2**

- **Stop, start or reboot instances.** Pick them by instance ID, or filter by tags and pick from the matches.
- **Pair a stop with a start.** Add the opposite action at a second time, for example stop at 21:00 and start at 07:00.
- **Resize Auto Scaling groups.** Set the minimum, maximum and desired size, for example to scale a group to zero overnight.
- **Dry run.** See which instances a schedule would affect, and their current state, before you save it.

**RDS**

- **Stop or start** RDS instances and Aurora clusters.
- **Take a snapshot before stopping**, and keep the last seven.
- **Pair a stop with a start** on a recurring schedule.
- **Skip databases already in the requested state.** A stop on a stopped database is recorded as skipped, not failed.
- **Pause and resume** a recurring schedule.

**Both**

- **Run now, once, or on a schedule** (hourly, daily, weekly, monthly, or a cron expression).
- **Request and approve.** Users who are not administrators submit schedules for an administrator to approve or reject.

## Who it is for

Platform, cloud and FinOps teams who pay for development, test or off-hours environments that sit idle overnight and at weekends, and want them off without writing their own scripts.

## Where to find it

After activation, a **Scheduler** section appears in the left menu:

| Menu item | What it is |
| --- | --- |
| **EC2** | EC2 instance and Auto Scaling group schedules. Create, view, edit, approve and delete them. |
| **RDS** | RDS instance and Aurora cluster schedules, with run history and snapshots. |

Schedules belong to the workspace they were created in.

## What it works with

| | |
| --- | --- |
| Cloud | AWS |
| Compute | EC2 instances and EC2 Auto Scaling groups |
| Databases | RDS instances and Aurora clusters |
| Scheduling | Amazon EventBridge Scheduler in your AWS account. RDS schedules also use small Lambda functions there. |
| Credential | An AWS scope attached to the workspace |
| Not covered | Other clouds, other AWS services, and terminating instances or changing their size. |

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need, how to activate Instance Scheduler, the AWS permissions it needs, and what it creates in your account. |
| [Use](use.md) | Schedule EC2 instances, Auto Scaling groups and RDS databases, approve requests, and check what ran. |
| [Permissions and Safety](permissions-and-safety.md) | What it can read and change, what needs approval, and what read-only users, regular users and administrators can do. |
| [Troubleshooting and FAQ](troubleshooting.md) | Error messages and how to fix them. |
