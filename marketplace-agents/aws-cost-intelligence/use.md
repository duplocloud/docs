---
description: Step-by-step walkthroughs of the main things AWS Cost Intelligence does.
---

# Use

## Add a dashboard

1. Open **FinOps > Cost Intelligence** and select a cost data source.
2. Select **Add dashboard** (in the source's more-actions menu).
3. Enter a **Name** and optional **Title**, then choose the **Dashboard** kind. The kind cannot be changed later; add a second dashboard instead.
4. Optionally set the **Default Date Range**, **Default Granularity**, **Default Cost Metric** and **Currency**.
5. Select **Create**. Start with **Cost and Usage**.

<!-- VERIFY: form labels from the Add dashboard component. Screenshot CI-07. Resource Ownership and Action Center are behind feature switches in code (both on); confirm they ship on. -->

Tag Attribution, Action Center and Resource Ownership each add AWS requests to every sync, so adding one needs the **Refresh cost data** permission. See [Permissions and Safety](permissions-and-safety.md).

## Work with a dashboard

- **Date range**: one control on every tab, with presets, any billing month or custom dates. A tab with monthly data says which months it used.
- **Filters**: each tab offers only the filters it can apply exactly. Date range, account and region carry over between tabs.
- **Summary tiles**: a tile with "View in" under it opens the tab that breaks the number down.
- **PDF**: the **PDF** menu exports the current tab or every tab.
- **Theme**: the light and dark switch applies to the whole extension.

## Refresh cost data

Syncs run on the source's schedule, every 6 hours by default. To run one now, select **Refresh data** on the source page (the list menu calls it **Refresh cost data**). Each refresh is billed by AWS, so you cannot start one while another is running or within 15 minutes of the last one, unless that one failed. The page says how long to wait.

<!-- VERIFY: the button reads "Refresh data" on the source page and "Refresh cost data" in the list menu; confirm which label to document. Screenshot CI-08. -->

## Work the Action Center

1. Add an **Action Center** dashboard to the source.
2. Use the tabs: **Overview**, **Open items**, **Realized**, **Back in use** and **Exclusions**. Open items are grouped by status, account or source, largest saving first.
3. Open an item to see its evidence, history and comments, then:
   - **Create ticket**: shows the ticket first (where it goes, the title and description). Nothing is created until you approve it. The item then moves to **In work**.
   - **Resolve**: you made the change. The next sync checks AWS's daily cost for that resource and moves the item to **Realized**, or to **Back in use** if it is still costing money.
   - **Exclude**: you will not act on it. A reason is required. **Restore** brings it back.
   - **Comment**: add a note for whoever picks it up.
4. In **Settings** choose where tickets go: Helpdesk, ClickUp or Jira.

A Helpdesk ticket is an analysis: an AI agent checks the finding with read-only AWS calls and writes a plan for a person to carry out. Each command it wants to run waits for your approval in the ticket. It never makes the change.

Once an item has a ticket, the Action Center keeps the ticket in step: it closes it when the item is realized, excluded or back in use, and reopens it if the item is open again.

<!-- VERIFY: behaviour is from docs/USER-GUIDE.md section 6 and 7 and the backend; button names from the item dialog were not all checked (screenshots CI-09 to CI-12). -->

## Policies

**Policies** on the source page lists every rule the dashboards flag resources by, each with a switch. Switching a rule off removes its items from the Action Center, the Optimisation and Idle and waste tabs and the KPI totals. Everyone who can see the source can read the policies; only a platform administrator can change them.

To add your own policy (administrators):

1. Select **Add policy** and describe it in your own words.
2. Select the rephrase and review step. An AI session with no AWS access rephrases it as a rule and lists what it assumed.
3. Review what the rule would flag against today's data, edit if needed, and select **Add policy**.

**Check accounts now** re-reads every account within two minutes, so a cleanup shows as resolved straight away. Policies only flag resources; nothing is changed in AWS.

<!-- VERIFY: step labels from docs/USER-GUIDE.md 6a; confirm in QA (screenshot CI-13). -->

## Build a custom dashboard

1. Select **Add dashboard**, choose **Custom - build from a prompt**, and describe what you want.
2. Review the **brief**: what will be built, what was assumed and what is not available. Choose **Build**, **Edit** or **Back**. Nothing is built until you confirm.
3. Refine it any time with **Update Dashboard**. Each build is shown for review and saved as a new version only when you save it. **Revision history** lets you **Revert** to any of the latest 20 versions.

Custom dashboards use the same data as the ready-made ones, so the figures match. Anything the data cannot answer is listed as not available, never estimated. Cost by tag is not available yet; use Tag Attribution.

## Ask AI

Select **Ask AI** in the dashboard header. A panel opens beside the dashboard. Ask about the spend, for example "why did EC2 go up last week?". Answers use the dashboard's own figures and, for more, read-only AWS queries that you approve. **Previous conversations** lists earlier sessions; each is a Helpdesk ticket.

See [Permissions and Safety](permissions-and-safety.md) for what is shared with the AI.

## Single account or organisation

A source on the management account shows every account and compares them. A source on one account hides the account comparisons and regroups by service or action. It is detected on each sync, or set with **Accounts covered**.
