# Access Control

## What is Access Control?

Access Control in DuploCloud AI Suite is the system that manages who can access the platform, what they can do, and which resources they can interact with. It allows administrators to define fine-grained permissions across users, workspaces, and AI agents — ensuring the right people have the right level of access.

---

## Users

A **User** is an individual account registered in the platform. Each user has an email address, a display name, and a role that determines their base level of access.

| Role | Description |
|---|---|
| **User** | Standard access — can interact with agents and resources within permitted scopes |
| **Administrator** | Full access — can manage all settings, users, groups, and permissions |

Users are created under the **User** tab in Access Control and can be added to Groups to inherit group-level permissions.

---

## Permission Sets

A **Permission Set** defines what a user or group is allowed to do within a specific workspace. It acts as a policy that controls access to scopes (resources) and agents.

Each permission set specifies:
- **Workspace** — which workspace the permissions apply to
- **Allowed Scopes** — the resources the user can access (e.g. `jira`, `aws-prod-scope`)
- **Denied Scopes** — resources explicitly blocked
- **Allowed Agents** — which AI agents the user can interact with (empty = all agents allowed)
- **Denied Agents** — AI agents explicitly blocked

Permission sets are created under the **Permissions** tab in Access Control and are assigned to groups.

---

## Groups

A **Group** is a collection of users that share the same permission sets. Instead of assigning permissions to each user individually, you assign a permission set to a group and add users to that group.

This makes it easy to manage access at scale — updating a group's permission set automatically applies to all users in it.

Each group has:
- A **name** and **description**
- One or more **Permission Sets** assigned to it
- One or more **Users** as members

Groups are created under the **Group** tab in Access Control.

---

## User Tokens

A **User Token** (API Token) is a secure credential that allows a user or an external system to authenticate with the DuploCloud AI Suite API without using a password. Tokens are commonly used for CI/CD pipelines, integrations, and automated scripts.

Each token has:
- A **name** to identify its purpose
- An **expiry date** — tokens must have a future expiry date and become inactive after it passes
- A **status** — either Active or Expired

> **Important:** The full token value is only shown once at creation time. Copy and store it securely — it cannot be retrieved again.

Tokens are managed on the **Profile** page, accessible from the profile icon in the top-right corner of the app.
