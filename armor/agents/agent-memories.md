# Agent Memories

Agent Memories give your DuploCloud AI agents **persistent, shared knowledge about a workspace** — facts, conventions, and preferences that the agent should already know every time it works on a ticket in that workspace, without you having to repeat them.

Unlike a single ticket's conversation history, a memory is:

* **Shared** — every ticket created in the workspace can use it, not just the one where it was written.
* **Persistent** — it doesn't expire or get summarized away. It's a plain Markdown file that stays until you edit or delete it.
* **Curated by you** — memories are written and maintained by admins, not silently inferred by the agent.

Each memory is a small Markdown file with a `type` that tells the agent (and other admins) what kind of knowledge it holds:

| Type | Use it for |
|---|---|
| `user` | Who the user is — role, preferences, expertise |
| `feedback` | How to work — corrections, confirmed approaches |
| `project` | Ongoing work, decisions, deadlines |
| `reference` | Pointers to external resources — dashboards, tickets, links |

Every workspace also has one special file, `MEMORY.md`, which is an index — a one-line summary of every memory the agent loads on every ticket. The full content of an individual memory file is only pulled in when the agent decides it's relevant.

---

## Step 1 — Open the Memories admin page

Memories are managed from **AI Admin**, not from inside a specific agent's workspace. Click the app switcher in the top left (it shows your current app, e.g. **AI DevOps**) and select **AI Admin**.

![](<../../../.gitbook/assets/agent-memories-step-01-app-switcher.png>)

![](<../../../.gitbook/assets/agent-memories-step-02-app-switcher-open.png>)

In **AI Admin**, select **Memories** from the left sidebar.

![](<../../../.gitbook/assets/agent-memories-step-04-sidebar-memories-highlight.png>)

## Step 2 — Pick a workspace

The Memories page shows one workspace's memory files at a time. Use the **Workspace** dropdown at the top to choose which workspace you want to manage.

![](<../../../.gitbook/assets/agent-memories-step-05-memories-page-overview.png>)

![](<../../../.gitbook/assets/agent-memories-step-06-workspace-selector.png>)

## Step 3 — Browse existing memories

The **FILES** panel on the left lists every memory file in the workspace. Click `MEMORY.md` to see the index the agent loads on every ticket — one line per memory, with its description and whether it was user-created or user-edited.

![](<../../../.gitbook/assets/agent-memories-step-07-memory-index-open.png>)

Click any other file to view or edit its full content in the editor on the right.

![](<../../../.gitbook/assets/agent-memories-step-08-memory-file-open.png>)

## Step 4 — Create a new memory

Click the **⋮** menu on the `memory` folder and choose **New memory**.

![](<../../../.gitbook/assets/agent-memories-step-09-folder-actions-menu.png>)

![](<../../../.gitbook/assets/agent-memories-step-10-add-memory-modal-empty.png>)

Fill in the form:

* **Name** — lowercase, hyphen-separated; this becomes the filename (`<name>.md`).
* **Description** — the one-line summary shown in `MEMORY.md`.
* **Type** — hover the info icon for a reminder of what each of the four types means.
* **Memory** — the actual content the agent should know.

![](<../../../.gitbook/assets/agent-memories-step-11-add-memory-name-filled.png>)

![](<../../../.gitbook/assets/agent-memories-step-12-add-memory-type-tooltip.png>)

![](<../../../.gitbook/assets/agent-memories-step-13-add-memory-type-options.png>)

![](<../../../.gitbook/assets/agent-memories-step-14-add-memory-filled.png>)

Click **Create**. The new file is saved, added to the `memory` folder, and automatically appended to the `MEMORY.md` index.

![](<../../../.gitbook/assets/agent-memories-step-15-memory-created.png>)

![](<../../../.gitbook/assets/agent-memories-step-16-new-file-in-tree.png>)

{% hint style="info" %}
Editing or deleting a memory works the same way — open the file to edit it and click **Save**, or use its **⋮** menu to **Download** or **Delete** it. Deleting a memory also removes its line from `MEMORY.md`.
{% endhint %}

## Step 5 — Turning memory off for a single ticket

Workspace memory is used by default, but any individual ticket can opt out. When creating a ticket, expand **Advanced Options** and use the **Workspace Memory** toggle.

![](<../../../.gitbook/assets/agent-memories-step-17-ticket-create-memory-toggle.png>)

This is useful for one-off tickets where you deliberately don't want the agent to bring in the workspace's usual context.

## Step 6 — Seeing a memory in action

Here's the `deploy-conventions` memory created above, being used on a real ticket. With **Workspace Memory** left on, a new ticket asks the agent about the team's deployment process:

![](<../../../.gitbook/assets/agent-memories-step-20-new-ticket-question-typed.png>)

The agent reads the memory and answers directly from it, without needing to be told the deployment process again:

![](<../../../.gitbook/assets/agent-memories-step-22-new-ticket-agent-response.png>)

The same **Workspace Memory** toggle is available on any open ticket's **Details** panel, so you can check or turn off memory for that specific conversation at any time:

![](<../../../.gitbook/assets/agent-memories-step-23-new-ticket-memory-toggle-panel.png>)
