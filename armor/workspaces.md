---
description: This is where it all comes together!
---

# Workspaces

A Workspace is the central entity that ties everything together — attach any number of Scopes and Personas to it. You can create multiple Workspaces and invite users to each one, enabling clear separation of responsibilities across your organization.

## Creating a Workspace

1. Navigate to **Workspaces** and click **Add Workspace**.

<figure><img src="../../.gitbook/assets/Workspaces-4.png" alt=""><figcaption></figcaption></figure>

2. Give the Workspace a **Name** and **Description**.
3. Select the **Persona(s)** to include in the Workspace, and click **Next**.

<figure><img src="../../.gitbook/assets/Workspaces.png" alt=""><figcaption></figcaption></figure>

3. Select the **Agent(s)** that do the work in this Workspace, and click **Next**.

<figure><img src="../../.gitbook/assets/Workspaces-1.png" alt=""><figcaption></figcaption></figure>

4. For each **Provider** screen, select the **Scopes** to include in the Workspace, then click **Next** until you have reviewed them all.

<figure><img src="../../.gitbook/assets/Workspaces-2.png" alt=""><figcaption></figcaption></figure>

5. Click **Create**.

**Congratulations!** Your Workspace is now ready to receive assignments, interpret goals, break down work, and provide a transparent audit trail—all with human oversight and control.

## Setting a System Prompt

Each Workspace can define a **System Prompt** — free-text instructions injected directly into the agent's system prompt on every ticket in that Workspace.

Open a workspace and go to the **Prompt** step (the same step where Prompt Suggestions and Prompt Templates are configured). Enter your instructions in the **System Prompt** field and save.

![System Prompt field on the Prompt step](../../.gitbook/assets/workspaces-step-01-system-prompt.png)

{% hint style="info" %}
This is distinct from [Agent Memories](agents/agent-memories.md). The System Prompt is a single field that's always injected verbatim into every ticket in the workspace. Memory is a set of files the agent reads on demand, and can be turned off per ticket. If the two conflict, persona instructions take precedence over the System Prompt.
{% endhint %}
