# Step 4: Configure Workspaces

A workspace is where your application's users do their work. It binds scopes (which IT systems they can access), personas (which skills the agent has available), and the users themselves. Every ticket, resource, and audit trail in your application belongs to a workspace — and every user action is traceable to the workspace it originated from.

## Creating a Workspace

Give the workspace a name and a description that reflects its purpose and audience. Names like "Platform Engineering", "L1 SRE", or "Sales Demand Gen" communicate scope at a glance and make it easy for administrators to reason about access boundaries as the organization grows.

## Attaching Scopes

Select which scopes the workspace can use. This determines which IT systems the agent can operate on when users in this workspace create tickets or resources. A workspace can have multiple scopes attached — for example, both an AWS production scope and a Datadog scope — so the agent can operate across systems in a single session.

Scopes are defined in Step 3 and are reusable across workspaces. Attaching a scope to a workspace does not duplicate the underlying credential; it simply makes that scope available for selection within the workspace.

## Assigning Personas

A persona is a bundle of skills. Assign one or more personas to the workspace to determine which skills the agent can use when executing tickets on behalf of users in this workspace.

For example, an SRE Persona might bundle troubleshooting, monitoring, and incident response skills. A Provisioning Persona might bundle Terraform and Kubernetes deployment skills. Personas can also include a system prompt that applies to all skills in the bundle, shaping the agent's overall behavior for that role.

Users do not select individual skills when creating a ticket — they select a persona. Personas are the abstraction that keeps the interface clean while giving administrators precise control over which capabilities are available to which teams.

## Inviting Users

Invite users to the workspace and assign RBAC roles. Permission sets define granular access rights — which scopes a user can select, which resource types they can create or modify, whether they can approve or only view. Permission set groups bundle multiple permission sets for easy assignment to roles like "read-only analyst" or "workspace administrator."

Every AI action in the workspace is traceable to a specific user using a specific scope, providing the auditability that regulated industries require.

## Example: Separation of Responsibilities

A concrete example from a DevOps organization illustrates how workspaces enforce separation of responsibilities:

An **L1 SRE workspace** has read-only access to infrastructure and codebase scopes, but write access to incident management (PagerDuty) and observability (Datadog) systems. It is assigned an SRE Persona that includes troubleshooting and monitoring skills. L1 engineers can investigate incidents, query logs, and update tickets — but they cannot modify cloud infrastructure or deploy workloads.

A **Platform Engineering workspace** has full write access to cloud infrastructure scopes and is assigned a Provisioning Persona with Terraform and Kubernetes skills. Platform engineers can provision Networks, Clusters, and Environments, and can manage the resource lifecycle end to end.

The same underlying providers and skills serve both teams. The workspaces — and the scopes and personas attached to them — determine what each team can actually do.
