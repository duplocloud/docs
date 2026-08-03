# Quotas

Quotas let administrators set cost limits on LLM usage. A quota definition sets the limit and period, and a quota mapping applies it to a specific context — at the ticket level, workspace level, or across the entire platform. When a limit is reached, the agent stops processing and reports the overage. All limits reset at UTC midnight.

***

## Quota Definitions

Go to **AI Admin → Access Control → Quota → Quota Definition**. This page lists all quota policies, showing their name, period type, and USD limit.

![](../../.gitbook/assets/quota-step-01.png)

### Add a Quota Definition

Click **+ Add**. Fill in the fields:

* **Name** — a unique identifier for the quota policy
* **Period Type** — how frequently the limit resets (e.g. Daily)
* **Limit (USD)** — the maximum spend allowed within the period

Click **Create**.

![](../../.gitbook/assets/quota-step-02.png)

***

## Quota Mappings

Click the **Quota Mapping** tab. Mappings bind a quota definition to a context and an Apply to value, determining which activity the limit applies to.

![](../../.gitbook/assets/quota-step-03.png)

***

## Add a Quota Mapping

Click **+ Add**. Fill in the fields:

* **Name** — a label for this mapping
* **Quota** — the quota definition to apply
* **Context** — whether this applies at the **Workspace** or **System** level
* **Target Workspace(s)** — one or more workspaces this mapping applies to (only shown when Context is Workspace — you can select multiple)
* **Apply to** — what the limit tracks. The available options depend on Context:

| Context | Apply to options | Meaning |
|---|---|---|
| System | All Workspaces And Users | Every workspace and every user, platform-wide |
| System | All Workspaces | Every workspace, platform-wide |
| System | All Users | Every user, regardless of workspace |
| Workspace | Above Selected Workspaces | Shared limit across all activity in the selected workspace(s) |
| Workspace | Per User In Selected Workspaces | A separate limit for each user, within the selected workspace(s) |
| Workspace | Per Ticket In Selected Workspaces | A separate limit for each ticket, within the selected workspace(s) |

### Ticket Quota

When **Apply to** is set to **Per Ticket In Selected Workspaces**, the quota limit applies per individual ticket. Each ticket has its own spend counter — one ticket reaching the limit does not affect other tickets in the same workspace.

![](../../.gitbook/assets/quota-step-05.png)

To verify, create a ticket in the target workspace and run a request.

![](../../.gitbook/assets/quota-step-07.png)

Once the ticket's cumulative cost hits the defined limit, the agent stops and returns an error showing the ticket ID, the amount used, and when the limit resets.

![](../../.gitbook/assets/quota-step-08.png)

Because the quota is scoped to the individual ticket, a new ticket created in the same workspace starts with a fresh counter and continues working normally.

![](../../.gitbook/assets/quota-step-09.png)

### Workspace Quota

When **Apply to** is set to **Above Selected Workspaces**, the quota limit applies to all activity within the selected workspace(s). The cumulative spend across all tickets in a given workspace counts toward that workspace's shared limit.

![](../../.gitbook/assets/quota-step-11.png)

Create a ticket and run a request in the workspace.

![](../../.gitbook/assets/quota-step-12.png)

Once the workspace's cumulative spend reaches the limit, the agent blocks all new requests within that workspace, reporting the workspace name, total used, and reset time.

![](../../.gitbook/assets/quota-step-13.png)

Switching to a different workspace bypasses the limit entirely — the quota is scoped to the specific workspace it was mapped to, so other workspaces are unaffected.

![](../../.gitbook/assets/quota-step-14.png)

A ticket in the new workspace runs successfully with its own independent cost counter.

![](../../.gitbook/assets/quota-step-15.png)

### User Quota

Set **Apply to** to **Per User In Selected Workspaces** (Context: Workspace) or **All Users** (Context: System) to give each user their own spend counter, independent of which ticket or workspace they're working in. One user hitting their limit doesn't affect any other user — including other users active in the same workspace or ticket.

### System Quota

When **Context** is set to **System**, the quota applies across the entire platform rather than specific workspaces. Set **Apply to** to **All Workspaces And Users** to enforce a single limit globally, or **All Workspaces**/**All Users** to cap just one of those dimensions platform-wide.

![](../../.gitbook/assets/quota-step-16.png)

Once a system-wide limit is reached, all matching agent requests across every workspace are blocked, regardless of which workspace, user, or ticket they originate from.

![](../../.gitbook/assets/quota-step-17.png)
