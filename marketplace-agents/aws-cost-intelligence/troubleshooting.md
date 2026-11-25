---
description: Common problems with AWS Cost Intelligence and how to fix them.
---

# Troubleshooting and FAQ

## Setting up

| What you see | What it means | What to do |
| --- | --- | --- |
| The scope isn't in the **AWS Scope** list | It isn't attached to this workspace. | Attach the scope to the workspace (see [Set Up](set-up.md#3-connect-aws-to-duplocloud)). |
| **Add Cost Data Source** is greyed out | Only a platform administrator can add, edit or delete cost data sources. | Ask an administrator. |
| The sync fails with "access denied" | The role, or its trust policy, is wrong. | Check that the billing role trusts the platform identity ARN. |
| The sync fails with "security token expired" or "the security token included in the request is invalid" | The credential uses temporary keys that have expired or can't be read. | Switch the provider to an IAM role credential, then select **Refresh data**. |
| The sync works but the dashboards are empty | Cost Explorer is still filling. | Wait up to 24 hours after turning it on. |
| "Filling in monthly breakdowns" on the source | Older months are still being pulled. | Nothing. It finishes over the next few syncs. |

## Data and dashboards

| What you see | What it means | What to do |
| --- | --- | --- |
| A tab names a missing action, such as `budgets:ViewBudget` | The role can't call it. | Add the action to the role, or update the stack to the latest template. The next sync picks it up. |
| Resource Explorer is empty, or resolved items are never confirmed | Resource-level data is off in Cost Explorer, or `ce:GetCostAndUsageWithResources` is missing. | Turn on **Resource-level data at daily granularity** and add the action. |
| The Optimisation tab and Action Center are empty | Cost Optimization Hub isn't enabled. | Enable it in the payer account, including member accounts. |
| A tag has no data | It isn't activated as a cost allocation tag. | Activate it in Billing. It appears after AWS's backfill. |
| Resource Ownership shows an account as not reached | The member role is missing there, its trust policy refuses the billing role, or the external ID is wrong. | Check the **Coverage** tab, which names the refused call. |
| "This couldn't be loaded right now", with a reference | That one view failed. The rest still works. | Try again. If it keeps failing, give the reference to your administrator. |

## Refreshing and access

| What you see | What it means | What to do |
| --- | --- | --- |
| **Refresh data** is refused ("already queued or running", or "can start in N min") | A sync is running, or the last one was less than 15 minutes ago. | Wait. A refresh after a failed sync is allowed straight away. |
| A page says you don't have access, or that something doesn't exist | You don't have read access to that source or dashboard, or it was deleted. | Ask an administrator for access, or go back to the list. |
| Buttons are greyed out, with the reason on hover | Your permission set doesn't allow that action. | Ask an administrator (see [Permissions and Safety](permissions-and-safety.md#who-can-do-what)). |
| "You don't have access to the scope ..." | The scope is attached to the workspace, but your permission set doesn't allow it. | Ask an administrator to allow it. |
| The sync fails, or Ask AI is refused, with "no longer attached to this workspace" | The source's AWS scope was detached. | Attach it again, or edit the source to choose another. |

## Action Center and tickets

| What you see | What it means | What to do |
| --- | --- | --- |
| A resolved item is still "awaiting refresh" | AWS's resource data lags by up to a day. | Wait for the next sync. |
| An item moved to **Back in use** | The resource is still costing money. | Check the resource. Resolve it again once it's removed, or exclude it with a reason. |
| "A ticket for this item is already being created" | Someone, or a second click, is creating it now. | Refresh the page in a moment. |
| A Helpdesk analysis can only confirm the cost, not the resource | No AWS scope is registered for the item's account. | Deploy the analysis role to that account. |
| Jira or ClickUp: "not attached to this workspace", "has no API token" or "cannot sign in" | The provider's scope or credential isn't set up. | Check the provider and attach its scope (see [Set Up](set-up.md#optional-send-tickets-to-jira-or-clickup)). |
| An item says it couldn't close or reopen its ticket | The Jira or ClickUp identity can create tickets but not comment on or move them. | Give it **Add comments** and **Transition issues** (Jira), or edit access to the List (ClickUp). |
| A Jira issue's history says "left off priority" | The project's create screen has no Priority field. | Add it to the screen, or turn off priority from saving in **Settings**. |
| Tickets have no link back to the Action Center | The portal's address isn't configured on the platform. | Ask your DuploCloud contact to set it. |

## FAQ

**Does it change anything in my AWS account?** No. It only reads. Helpdesk tickets are analyses with a plan for a person to carry out.

**How fresh is the data?** Syncs run every 6 hours by default. You can change the schedule on the source, or refresh by hand.

**Does it work in GovCloud or China?** No. Only AWS commercial regions.

**Can I cover one account instead of an organization?** Yes. Use a role in that account. The dashboards then leave out account comparisons.

**Who can add a cost data source?** A platform administrator.

**Who can refresh the data?** Someone with `finops.sync` and edit rights on the source or one of its dashboards.

**Does Ask AI change anything?** No. It answers from the dashboard's figures, and any AWS read it needs waits for your approval.

**What happens if I delete a source?** Its cost data, dashboards and Action Center decisions are removed. Tickets already created stay in their own systems.
