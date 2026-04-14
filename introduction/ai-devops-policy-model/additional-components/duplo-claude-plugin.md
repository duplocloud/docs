# Duplo Claude Plugin

---
description: >-
  Use Claude Code in your terminal or IDE to work on DuploCloud projects
  with ticket-driven workflow enforcement.
---

# Claude Code Plugin

The DuploCloud Claude Code Plugin connects Claude Code — whether you run it in the terminal or inside your IDE — directly to DuploCloud's AI Helpdesk. It enforces a ticket-driven development workflow: every session is tied to an active project or ticket, and all work proceeds through a spec and an implementation plan that are stored and approved on the DuploCloud platform.

This means that when you ask Claude to make changes, it already knows what project you're working on, what the approved requirements are, and what the plan says should happen. The result is AI-assisted DevOps that stays aligned with your team's intentions and leaves a full audit trail on the platform.

## Prerequisites

* [Claude Code](https://claude.ai/code) installed
* Access to a DuploCloud instance with AI HelpDesk enabled

## Installation

Please refer to the instructions here: 
[Duplo Claude Plugin](https://github.com/duplocloud/duplo-claude-plugin)


## Quickstart

The workflow has two phases: **planning** (spec and plan) and **execution** (working through plan tasks). Run these in order within your project directory:

**Planning phase:**

1. `/duplo:activate_project` — Log in and set your active project.
2. `/duplo:activate_ticket` — Create or resume a ticket for your current work phase.
3. `/duplo:write_spec` — Collaboratively draft and approve a project specification.
4. `/duplo:write_plan` — Draft and approve an implementation plan based on the spec.

**Execution phase** (once the plan is approved):

5. `/duplo:activate_ticket` — Select an execution task from the approved plan and open a ticket for it.
6. `/duplo:save_summary` — Save a summary of the work done on the active ticket to the platform.

Each command is interactive — Claude will guide you through the steps and prompt you for input as needed. See the [Full Workflow Reference](#full-workflow-reference) below for detailed documentation on each command.

---

## Full Workflow Reference

### `/duplo:activate_project`

**What it does:** Authenticates you with your DuploCloud instance, sets your active workspace and project, and downloads the latest spec and plan from the platform into your local `.duplocloud/` directory. Ends with a health summary showing whether the project has an approved spec, an approved plan, or neither.

**When to run it:** At the start of every session, or any time you need to switch projects or workspaces.

**Step-by-step:**

1. The plugin checks for an active workspace in your current state.
   * If a workspace is already set, Claude asks whether to continue with that workspace or switch.
   * If you continue with the same workspace and a project is already active, Claude separately asks whether to continue with that project or switch. (If you switch workspaces, the project is always reset and you will be prompted to select a new one.)
2. If no credentials are found, the plugin opens a credentials file in your editor for you to fill in your DuploCloud base URL and API token, then saves and closes it. If an editor is not available, a terminal command is shown instead.
3. If multiple workspaces are associated with your account, Claude presents the list and asks you to select one. If only one workspace exists, it is selected automatically.
4. Claude lists the projects available in that workspace and asks you to select one.
5. The plugin downloads the current spec and plan from the platform and saves them locally to `.duplocloud/spec.md` and `.duplocloud/plan.md`:
   * **Resuming the same project:** If neither local file exists, files are downloaded silently. If one or both local files already exist, Claude asks whether to overwrite them with the latest versions from the platform.
   * **Switching to a new project:** Local files are always overwritten with the new project's content without prompting.
6. Claude displays a project health summary based on the platform's current state:

   | Artifact | Status |
   |----------|--------|
   | Spec | Approved / Draft (local file exists) / Not started |
   | Plan | Approved / Draft (local file exists) / Not started |

7. Depending on the platform state, Claude offers next steps:
   * Spec phase (not yet started or in draft) → offers to proceed to `/duplo:activate_ticket` for spec creation.
   * Plan phase (spec approved, plan not yet started or in draft) → offers to proceed to `/duplo:activate_ticket` for plan creation.
   * Both approved → tells you the project is complete; no further action is needed.

---

### `/duplo:activate_ticket`

**What it does:** Determines your current work phase and activates the right ticket for it. Supports two modes: **planning** (spec/plan creation) and **execution** (working through tasks from an approved plan). Loads past conversation context from the platform when resuming an existing ticket.

**When to run it:** After activating a project — both at the start of the planning phase and when picking up an execution task.

**Step-by-step:**

1. The plugin checks the current project state.
   * If no active project is found, Claude asks if you'd like to activate one now.
2. If the project has execution tasks ready (i.e., the plan is approved and broken into tasks), Claude asks:
   * **Yes — pick an execution task** → continue to step 3.
   * **No — resume planning work** → skip to step 6.
   * If no execution tasks exist, the plugin goes directly to step 6 (planning mode).
3. **Execution task selection:** Claude lists the available tasks.
   * If there are more than 10 tasks, Claude first asks you to select a stage, then shows the tasks within it.
   * If there are 10 or fewer tasks, all tasks are shown in a flat list with their stage and current ticket status.
4. Select a task by number. If a ticket already exists for that task, it is resumed (skip to step 5). If not, Claude presents the list of available AI Agents and asks you to select one, then creates a new ticket linked to that task.
5. The ticket is moved to **In Progress** on the platform. Claude loads the mirrored conversation history from any prior sessions on this ticket, summarises where things left off, and stops — you are now ready to work.
6. **Planning mode:** The plugin searches the platform for an existing open spec/plan ticket.
   * **Existing ticket found:** It is activated, past context is loaded, and the command completes. Run `/duplo:write_spec` or `/duplo:write_plan` to continue.
   * **No ticket found:** Claude presents the list of available AI Agents, asks you to select one, and creates a new ticket. The ticket is moved to **In Progress** and Claude automatically proceeds to `/duplo:write_spec` or `/duplo:write_plan` based on the current phase.

{% hint style="info" %}
When resuming any existing ticket, Claude loads the full mirrored conversation history from the platform so it can pick up exactly where the previous session left off.
{% endhint %}

---

### `/duplo:write_spec`

**What it does:** Guides you through drafting a project specification collaboratively with Claude, then lets you save or approve it on the DuploCloud platform.

**When to run it:** After activating a spec ticket. Requires an active spec ticket — if none exists, Claude will prompt you to run `/duplo:activate_ticket` first.

**Step-by-step:**

1. The plugin checks for an active spec ticket. If none exists, it stops and prompts you to run `/duplo:activate_ticket` first.
2. The plugin fetches any existing spec content from the platform:
   * **No existing spec:** Claude asks, "What would you like to achieve as part of this project?" and then asks clarifying questions one at a time to build up an understanding of your requirements.
   * **Existing spec found:** Claude shows you the current draft and asks whether you'd like to continue refining it or start fresh.
3. Claude drafts the spec and shows it to you. You can request changes — Claude will revise and re-present until you're satisfied. The draft is saved to `.duplocloud/spec.md` each time it is updated during this revision loop.
4. Once you're satisfied, Claude asks how you'd like to proceed:

   | Option | What happens |
   |--------|-------------|
   | **Save** | Pushes the spec to the platform in Draft status. |
   | **Save and Approve** | Pushes the spec and marks it as Approved, unlocking the plan phase. |
   | **Cancel** | Keeps the local draft only; nothing is pushed to the platform. |

{% hint style="info" %}
The spec must be **Approved** on the platform before you can move to `/duplo:write_plan`. Use **Save and Approve** when your spec is ready, or return later and re-run `/duplo:write_spec` to approve a previously saved draft.
{% endhint %}

---

### `/duplo:write_plan`

**What it does:** Guides you through drafting a detailed implementation plan based on your approved spec, then lets you save or approve it on the DuploCloud platform.

**When to run it:** After the spec is approved and a plan ticket is active. Requires an active plan ticket — run `/duplo:activate_ticket` if one doesn't exist yet.

**Step-by-step:**

1. The plugin checks for an active plan ticket. If none exists, it stops and prompts you to run `/duplo:activate_ticket` first.
2. The plugin fetches the approved spec for context, so Claude understands the requirements and scope.
3. The plugin fetches any existing plan content from the platform:
   * **No existing plan:** Claude asks, "The spec is loaded. What aspects of the implementation would you like to focus on, or shall I draft a complete plan from the spec?" and asks clarifying questions to inform the plan.
   * **Existing plan found:** Claude shows you the current draft and asks whether to continue refining it or start fresh.
4. Claude drafts the implementation plan, structured as numbered tasks with steps and expected outputs.
5. Claude shows you the draft. You can request changes — Claude revises and re-presents until you're satisfied. The draft is saved to `.duplocloud/plan.md` each time it is updated during this revision loop.
6. Once you're satisfied, Claude asks how you'd like to proceed:

   | Option | What happens |
   |--------|-------------|
   | **Save** | Pushes the plan to the platform in Draft status. |
   | **Save and Approve** | Pushes the plan and marks it as Approved. |
   | **Cancel** | Keeps the local draft only; nothing is pushed to the platform. |

---

### `/duplo:save_summary`

**What it does:** Generates a structured markdown summary of the work done on the current active ticket and saves it to the DuploCloud platform.

**When to run it:** At any point during or after completing work on a ticket, when you want to record a summary. Must be triggered explicitly — Claude will not save a summary automatically when work is finished.

{% hint style="info" %}
To trigger this command, explicitly ask Claude: "save summary", "update summary", or "summarise the work". Completing tasks or passing tests does not auto-trigger a summary save.
{% endhint %}

**What the summary includes** (sections are omitted if not relevant):

| Section | Contents |
|---------|----------|
| **Summary** | 2–3 sentences on what the ticket was about and what was accomplished. |
| **Completed** | Bullet list of things successfully done. |
| **What Went Wrong** | Issues, errors, or blockers encountered, with root cause where known. |
| **Approach Changes** | Pivots from the original plan — what changed, why, and impact on future tasks. |
| **Discoveries** | Concrete findings uncovered (resource names, configurations, technical facts). |
| **Key Decisions** | Important technical or architectural decisions made. |
| **Future Task Impacts** | Specific impacts on upcoming tickets the project lead must account for. |
| **Open Items** | Unresolved issues, pending questions, or follow-up actions still needed. |

**Step-by-step:**

1. Claude confirms: "Shall I save a summary of this work to the ticket? (y/n)"
2. If confirmed, Claude generates the summary covering only the current active ticket's work.
3. The summary is pushed directly to the platform. Claude confirms: "Summary saved to the ticket."

---

### `/duplo:deactivate`

**What it does:** Clears your DuploCloud credentials and active project context from the local environment. Claude returns to its normal behavior without any DuploCloud enforcement.

**When to run it:** When you're done working on DuploCloud projects, or when you want to switch DuploCloud instances.

**Step-by-step:**

1. Claude confirms: "This will clear your DuploCloud credentials and project context. Continue? (yes/no)"
2. If confirmed, the following are removed:
   * `~/.duplocloud/.auth` — your stored credentials
   * `.duplocloud/state.json` in your current working directory — the active project context
3. Claude confirms: "DuploCloud deactivated. Claude is back to normal behavior."

{% hint style="info" %}
Deactivation only removes credentials and active state. Your local `.duplocloud/` directory — including `spec.md` and `plan.md` — is preserved. Re-activate at any time with `/duplo:activate_project`.
{% endhint %}

---

## Ticket Lifecycle

These behaviors are built into the plugin and apply during any active ticket session.

**Closing a ticket:** To close a ticket, explicitly ask Claude — for example, "close the ticket", "mark as done", or "resolve the ticket". Claude will confirm before closing. Phrases like "all done" or "finished" do not trigger a close automatically.

**Saving a summary:** Use `/duplo:save_summary` or ask Claude explicitly to save a summary. Completing tasks, running tests, or finishing an implementation does not auto-trigger a summary save.

**Work Done summaries:** After every response in which meaningful work was done — code written, files changed, commands run, decisions made — Claude automatically appends a brief **Work Done** section to its reply. This is a running record of actions taken within the session.

**Session state errors:** If your session state goes missing mid-session (e.g., after a restart), Claude will not attempt to re-activate automatically. It will prompt you to run `/duplo:activate_ticket` to restore context.

---

## Background Behavior

The plugin runs two operations automatically, without requiring any action from you:

**CLI tool installation:** On your first prompt after installing the plugin, the required Python CLI tools are installed to `~/.duplocloud/bin/`. This happens once and is transparent.

**State mirroring:** After every prompt you submit and at the end of each Claude session, the plugin mirrors your local project state back to the DuploCloud platform in the background. This keeps the platform in sync with your local work without any manual push steps.

**Completion reminders:** At the end of each Claude session, the plugin runs a completion check that may surface a reminder message. This is triggered by the plugin, not by Claude itself.
