---
description: Activate agents from the Agent Marketplace, and build your own in Agent Studio.
---

# Agents

{% hint style="info" %}
This page reflects an in-progress rename: **Extensions** is becoming **Agents** in the portal. The change is merged but not yet in a release. If your sidebar still says **Extensions** and **Studio**, the same screens are there under the old names.
{% endhint %}

Agents add capabilities to the platform — API resources, menu entries, and skills — loaded at runtime without redeploying the portal. Whether you activate one from the Marketplace or build your own, the portal calls it an **agent**. The only place the old name remains is the package you upload, `extension.zip`.

There are two places to work with agents, and they do different jobs:

|                       | Where                               | What it's for                                                   |
| --------------------- | ----------------------------------- | --------------------------------------------------------------- |
| **Agent Marketplace** | **AI Admin → Marketplace**          | Activate published agents and manage what's running on the platform |
| **Agent Studio**      | **Agent Studio** within a workspace | Build a new agent from a description                            |

Start with the Marketplace — activating something that already exists needs no source control and no build.

***

## Activating an agent

Go to **AI Admin → Marketplace**. The **Agents** page has two tabs: **Activated Agents** and **Agent Marketplace**.

### Activated Agents

Summary tiles across the top show how many agents are activated (with how many are active, disabled or failed), how many need attention, and when the set last changed. The table is grouped into a tab per agent; anything that doesn't belong to an agent appears under **Other**. Each table lists the name, **Agent Id**, version, status, resource count, the menus it adds, whether it is tracked in source control, and when it was last updated.

![Activated Agents](../.gitbook/assets/extensions-step-01-activated-agents.png)

Use the search box and the **All statuses / Active / Disabled / Failed** filters to narrow the list — **Failed** is the one to check when an agent's resources or menus aren't appearing.

### Agent Marketplace

The **Agent Marketplace** tab is the catalog of agents you can activate. Search agents by name, or filter by category, and use **Refresh** to re-read the catalog. **Recommended for you** highlights a few agents at the top. Each card shows the agent's category, a one-line summary of what it does, its status, and an **Activate** button.

![Agent Marketplace](../.gitbook/assets/extensions-step-02-agent-marketplace.png)

Click an agent to open its details: what it does, its version and category, and **Where it lives in your nav** — the left-nav position it will take, which you can **Change** before activating. The details panel also lists the publisher and the **Manifest ID**.

![Agent details](../.gitbook/assets/extensions-step-03-agent-details.png)

Click **Activate** to add the agent. On a portal connected to the DuploCloud console, the first **Activate** of a free agent opens the console in a new tab, where you accept the Marketplace terms. The console then sends you back to the portal to choose where the agent appears in your nav, and the install starts. In the DevKit, free agents activate straight from the portal.

Once an agent is active, its details offer **Open** to go to it and **Deactivate** to turn it off, plus **Update** when a newer version is available.

{% hint style="info" %}
If the catalog shows **No agents are published yet**, or a banner says the agent catalog is unreachable or no license is installed, the platform can't load the catalog — check the platform's license and its connection to DuploCloud.
{% endhint %}

### Inspecting an activated agent

Opening an agent from the **Activated Agents** table shows what it actually contributes to the platform.

![Agent detail](../.gitbook/assets/extensions-step-04-extension-detail.png)

The header carries its status, **Agent Id**, version, and last-updated time. Below that:

* **Load Context** — the fully-qualified identifier and version the platform loaded
* **Source Control** — the repository it is tracked in, or **Not tracked** for a zip upload
* **Menu Entries** — how many navigation entries it adds
* **Skills** — the skills it registers, with their fully-qualified paths
* **Resources** — the API resources it registers, by origin type, sub-type, and REST segment

Three tabs give more detail: **Overview** (above), **Menu** (the navigation entries it adds), and **Manifest** (the raw declaration).

The **Actions** menu on the detail page lets you **Disable** an agent without removing it — its resources and menus stop loading, and the status changes to Disabled — or **Enable** one that is currently disabled. **Delete** unloads the agent and removes its record. Each asks for confirmation first. The same actions are on each row's menu in the table, where delete is labelled **Delete Agent**.

### Registering an agent from a file

If you have a built agent that isn't in the catalog, click **Register**. The **Register agent** dialog asks for its `extension.zip`.

![Register agent](../.gitbook/assets/extensions-step-05-register-modal.png)

The agent is hot-loaded without a restart. Agents registered this way show **Not tracked** under Source Control, since there's no repository behind them.

***

## Building an agent in Agent Studio

Agent Studio is the authoring side, scoped to a workspace rather than the platform. Go to **Agent Studio** in the workspace navigation. It lists the agents being built in the workspace, with tiles for the total, how many are ready, in progress, or need attention.

![Agent Studio](../.gitbook/assets/extensions-step-06-agent-studio.png)

Click **New Agent**. The form has two steps.

**Details:**

* **Agent name** — becomes the resource type, generated like a built-in resource
* **Icon** — the menu icon for the generated resource
* **Scopes** _(optional)_ — credentials the agent uses to test the new resource's APIs while building
* **Use source control** — off by default. Off, the agent builds a throwaway copy and hot-loads it. On, the agent is authored inside your Git repository, and you also provide:
  * **Repository scope** — a GitHub scope; the agent clones, commits, and pushes with its credentials
  * **Git organization**, **Repository** (type a name to use one that doesn't exist yet), and **Branch**

![New Agent](../.gitbook/assets/extensions-step-07-new-extension.png)

**Requirements:** describe what the agent should do, in Markdown, and optionally attach requirement files. Click **Next** to move from Details to Requirements, and **Back** to revise.

Clicking **Create & Build** starts a build that writes your agent against your requirements and loads it into the platform. You can refine the details in the provisioning ticket, where an **Agent Preview** shows the result once it's loaded.

Once built, an agent's detail page in Agent Studio shows its **Agent ID** and has:

* **Spec / Result** — switch between what you asked for and what was built
* **Ask the Agent** — reopen the provisioning ticket to keep working on it
* **Source control** tab — review changes, then **Commit…**, **Push changes**, or **Resync** with the remote (when source control is on)
* **Deprovision** — tears the agent back down, removing what it contributed

{% hint style="info" %}
Source control is optional. Turn it on when you want the agent's code kept in your own GitHub repository; leave it off to build and hot-load a copy without one. If you only want to use an agent someone else has published, activate it from the **Agent Marketplace** instead.
{% endhint %}

***

## Which one should I use?

* **Activate from the Agent Marketplace** when the capability already exists. No build, no repository, no scope.
* **Register a zip** when you have a built agent that isn't published to the catalog.
* **Build in Agent Studio** when you need something that doesn't exist yet — with source control on if you want to maintain it in your own repository.

To build your first agent step by step, see [Build Your Own Agent](../getting-started/build-your-own-agent/README.md).
