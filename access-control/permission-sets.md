# Create Permission Set Tutorial

This document explains how to create a new Permission Set in the DuploCloud AI Suite Access Control panel.

---

## Prerequisites

- Access to the DuploCloud AI Suite admin panel
- Admin permissions on the Access Control section

---

## Step 1 — Navigate to Access Control

Go to **AI Admin → Access Control** in the left-hand navigation. The page opens on the **Permissions** tab by default, which lists all existing permission sets.

![Step 1 — Permissions tab](../.gitbook/assets/permission-sets-step-01-permissions-tab.png)

---

## Step 2 — Click "Add"

In the top-right corner, click the **+ Add** button. The Add Permission Set form slides in.

![Step 2 — Add Permission Set form](../.gitbook/assets/permission-sets-step-02-form-opened.png)

---

## Step 3 — Enter a Name

Click the **Name** field and type a name for the permission set.

In this example: `QA-Test-Permission-Set`

![Step 3 — Name filled](../.gitbook/assets/permission-sets-step-03-name-filled.png)

---

## Step 4 — Enter a Description

Click the **Description** textarea and describe the purpose of this permission set.

![Step 4 — Description filled](../.gitbook/assets/permission-sets-step-04-description-filled.png)

---

## Step 5 — Open the Workspace Permission Modal

Click **+ Add Workspace Permission**. A modal dialog opens with fields for:

| Field | Purpose |
|---|---|
| Workspace | The workspace this permission applies to |
| Allowed Scopes | Resources the user can access |
| Denied Scopes | Resources explicitly blocked |
| Allowed Agents | AI agents the user can use (empty = all allowed) |
| Denied Agents | AI agents explicitly blocked |

![Step 5 — Add Workspace Permission modal](../.gitbook/assets/permission-sets-step-05-workspace-modal.png)

---

## Step 6 — Select the Workspace

Click the **Workspace** dropdown and select the target workspace.

In this example: `Production-DevOps`

![Step 6 — Workspace selected](../.gitbook/assets/permission-sets-step-06-workspace-selected.png)

---

## Step 7 — Select Allowed Scopes

Click the **Allowed Scopes** dropdown and select the scopes to grant access to. You can select multiple.

In this example: `jira` and `aws-prod-scope`

![Step 7 — Scopes selected](../.gitbook/assets/permission-sets-step-07-scopes-selected.png)

---

## Step 8 — Allow All Agents

Leave the **Allowed Agents** field empty to allow access to all agents. No selection is required.

![Step 8 — Agents left empty (all allowed)](../.gitbook/assets/permission-sets-step-08-agents-all.png)

---

## Step 9 — Confirm the Workspace Permission

Click the **Add** button inside the modal to save the workspace permission entry.

![Step 9 — Workspace permission added](../.gitbook/assets/permission-sets-step-09-workspace-permission-added.png)

---

## Step 10 — Submit the Form

Review the completed permission set form, then click **Create Permission Set**.

![Step 10 — Before submit](../.gitbook/assets/permission-sets-step-10-before-submit.png)

A green **Success** toast confirms the permission set was saved.

![Step 11 — After submit](../.gitbook/assets/permission-sets-step-11-after-submit.png)

---

## Step 11 — Verify in the List

The new permission set appears at the top of the Permissions table with the associated workspace.

![Step 12 — Final permissions list](../.gitbook/assets/permission-sets-step-12-final-list.png)
