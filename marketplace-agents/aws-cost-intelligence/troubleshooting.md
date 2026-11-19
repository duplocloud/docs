---
description: Common problems with AWS Cost Intelligence and how to fix them.
---

# Troubleshooting and FAQ

## Common problems

| What you see | What it means | What to do |
| --- | --- | --- |
| **A page says you do not have access, or that something does not exist** | You lack read access to that source or dashboard, or it was deleted. | Ask a workspace administrator for access, or go back to the list. |
| **Buttons are disabled with "read-only access"** | Your permission set does not allow that action. | Ask an administrator (see [Permissions and Safety](permissions-and-safety.md)). |
| **"Only a platform administrator can add, edit or delete cost data sources"** | Source changes are for platform administrators. | Ask an administrator. |
| **"You don't have access to the scope ..."** | The scope is attached to the workspace but your permission set does not allow it. | Ask an administrator to allow it. |
| **Sync Failed, "security token expired"** | The AWS credential's temporary keys expired. | Update the provider's credential, then select **Refresh data**. |
| **Sync Failed, "access denied"** | The role or its trust policy is wrong. | Check the role and its trust policy. |
| **Sync Failed or Ask AI refused, "no longer attached to this workspace"** | The source's AWS scope was detached. | Re-attach the scope, or edit the source to choose another. |
| **A tab says an action is missing, such as `budgets:ViewBudget`** | The credential cannot call it. | Add the action to the role. |
| **"Filling in monthly breakdowns..." on the source** | Older months are still being pulled. | Nothing. It finishes over the next few syncs. |
| **Resource Explorer is empty, or resolved items are never confirmed** | Resource-level data is off in Cost Explorer, or `ce:GetCostAndUsageWithResources` is missing. | Turn it on and add the action. |
| **Optimisation tab and Action Center are empty** | Cost Optimization Hub is not enabled. | Enable it in your payer account. |
| **Refresh refused ("already queued or running" or "can start in N min")** | Each refresh is billed by AWS, so there is a cooldown of 15 minutes. | Wait, or retry if the last sync failed. |
| **Resolved item still "awaiting refresh"** | AWS resource data lags by up to a day. | Wait for the next sync. |
| **Item moved to Back in use** | The resource is still costing money. | Check the resource. Resolve again once it is removed, or exclude it with a reason. |
| **Tag data missing for a tag** | The tag is not activated as a cost allocation tag. | Activate it in Billing. It appears after AWS's backfill. |
| **Resource Ownership shows an account as not reached** | The member role is missing there, its trust policy refuses the billing credential, or the external ID is wrong. | Check the **Coverage** tab, which names the refused call. |
| **"A ticket for this item is already being created"** | Someone, or a second click, is creating it now. | Refresh in a moment. |
| **Helpdesk ticket can only confirm cost, not the resource** | No AWS scope is registered for the item's account. | Deploy the analysis role to that account. The extension connects it automatically, or use **Member accounts for analysis > Connect now** as an administrator. |
| **"This couldn't be loaded right now" with a reference** | That one view failed. The rest still works. | Try again. If it keeps failing, give your administrator the reference. |
| **Jira: "No Jira provider is attached to this workspace"** | No Jira provider has a scope on this workspace. | Check the provider's name and attach its scope. |
| **Jira 401, or "Atlassian refused the service account's OAuth 2.0 credential"** | The credential is wrong, revoked or expired. | Create a new credential and update the provider. |
| **ClickUp 401 or 403** | The token was regenerated, or the bot cannot see the List. | Generate a new token, or share the List with the bot. |
| **Links from tickets back to the item are missing** | The portal address is not configured on the platform. | A platform administrator sets `Authentication__FrontendBaseUrl`. |

<!-- VERIFY: messages and causes are from docs/USER-GUIDE.md section 10, the extension README and the code. Confirm user-visible wording in QA. -->

## FAQ

**Does it change anything in my AWS account?** No. It only reads. Helpdesk tickets are analyses with a plan for a person to carry out.

**How much does it cost to run?** The AWS bill for Cost Explorer requests is about US$70 a month for a 45-account organisation on the default schedule. See [Set Up](set-up.md). <!-- VERIFY: price of the agent itself is not in the repo. -->

**How fresh is the data?** Syncs run every 6 hours by default. You can change the schedule on the source, or refresh by hand.

**Does it work in GovCloud or China?** No. Commercial AWS regions only.

**Can I cover one account instead of an organisation?** Yes. Use a role on that account. The dashboards then leave out account comparisons.

**Who can add a cost data source?** A platform administrator.

**Who can refresh the data?** Someone with `finops.sync` and edit rights on the source or a dashboard.

**Does Ask AI change anything?** No. It only suggests, and every AWS command waits for your approval.

**What happens if I delete a source?** Its cost data, dashboards and decisions are removed. Existing tickets stay in their own systems.

<!-- VERIFY: FAQ list is a first guess. The owner to add the questions customers actually ask. -->
