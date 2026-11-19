---
description: Stop and start EC2 and RDS on a schedule, and stop paying for idle resources.
icon: robot
---

# Instance Scheduler

Cut idle cost by switching AWS compute and databases off when nobody needs them. Instance Scheduler stops, starts or reboots EC2 instances, resizes Auto Scaling groups, and stops or starts RDS databases and Aurora clusters, immediately, once at a set time, or on a recurring schedule.

{% hint style="warning" %}
Instance Scheduler stops, starts and reboots real instances and databases in your AWS account. Only administrators can create schedules that run directly. Requests from other users wait for an administrator to approve them. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

<!-- VERIFY: the repo README says non-administrators are view-only, but the code at commit 4299c28 (v1.7.39) lets non-administrators submit requests that an administrator approves. This page follows the code. Owner (Yash Jain) to confirm the final design: admin-only or request-and-approve (ClickUp 17twvjx4bm2). -->

## What it does

Instance Scheduler adds a **Scheduler** section to the menu with two lists, **EC2** and **RDS**.

**EC2 schedules**

- **Stop, Start or Reboot** EC2 instances. Pick instances by ID or by tag rules.
- **Change Auto Scaling group capacity** (minimum, maximum and desired size), for example to scale a group to zero overnight. Optionally schedule a restore time.
- **Pair actions**: for Stop and Start, you can add the opposite action at a second time (for example stop at 21:00, start at 07:00).
- **Dry run** shows what a schedule would affect before you save it.

**RDS schedules**

- **Stop or Start** RDS instances and Aurora clusters.
- **Take a snapshot before stopping** (optional).
- **Pair a Start with a Stop** on the same recurring schedule.
- Targets that are already in the requested state are skipped.

Each schedule can run **now**, **once** at a chosen time, or **recurring** (daily, weekly, monthly, every N hours, or a custom cron expression).

<!-- VERIFY: in the EC2 form, "Execute now" is offered only for Auto Scaling group capacity changes (instance power actions offer One-time and Recurring). Confirm that is intended. -->

## Who it is for

Platform and cloud administrators who want to cut idle cost in development, test or off-hours environments without writing their own scripts.

## What it works with

| | |
| --- | --- |
| Clouds | AWS |
| Compute | EC2 instances and EC2 Auto Scaling groups |
| Databases | RDS instances and Aurora clusters |
| Scheduling | AWS EventBridge Scheduler in your own AWS account |
| Credentials | An AWS credential scope in your workspace |

<!-- VERIFY: the code still contains a second "DuploCloud mode" (credentials fetched from a DuploCloud tenant instead of an AWS scope). The EC2 form hides the mode picker for new schedules, but the backend, a background schedule runner and the setup script still support it, and the release-1 plan is to remove it. This draft documents only the AWS scope mode. Confirm what ships. -->

<!-- VERIFY: Auto Scaling group scheduling works in AWS scope mode in this code (EventBridge Scheduler calls the Auto Scaling API directly). The Slack note said ASG claims were removed because they only worked in DuploCloud mode; the code contradicts that. Confirm whether ASG stays in the docs. -->

<!-- VERIFY: free or paid. The repo does not say; the Release 1 listing decides. -->

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need before you start, how to activate Instance Scheduler from the Agent Marketplace, and the AWS permissions it needs. |
| [Use](use.md) | Step-by-step walkthroughs of the main things Instance Scheduler does. |
| [Permissions and Safety](permissions-and-safety.md) | What Instance Scheduler can read and change, which actions need approval, and how it behaves for read-only, regular and admin users. |
| [Troubleshooting and FAQ](troubleshooting.md) | Common problems with Instance Scheduler and how to fix them. |
