# Create a Ticket Tutorial

This document explains how to create a new ticket in the DuploCloud AI Suite HelpDesk, configure the agent's model, scopes, permissions and context, and work with the agent on the resulting ticket page.

---

## Prerequisites

- Access to the DuploCloud AI Suite
- An authenticated user account
- At least one scope configured in the system

---

## Step 1 — Navigate to Add Ticket

Go to **HelpDesk** in the left-hand navigation and click **Add Ticket**. The page asks a single question — *What should the agent work on?* — with the task description box, the controls for this ticket, and an **Agent loadout** summary beneath it.

![Add Ticket page](../../.gitbook/assets/ticket-v2-step-01-add-ticket-page.png)

---

## Step 2 — Choose the model (optional)

The button below the task box shows the model and SDK that will handle this ticket. Click it to pick a different one.

![Model and SDK selector](../../.gitbook/assets/ticket-v2-step-02-model-picker-closed.png)

The list shows every model available to your workspace, with the underlying model ID and the SDK that runs it. Which models appear here is governed by the workspace's [LLM mappings](agents/llm-models.md#llm-mappings).

![Model list open](../../.gitbook/assets/ticket-v2-step-03-model-picker-open.png)

---

## Step 3 — Select scopes (optional)

Click **Select Scopes** to choose the credentials the agent may use. A **scope** defines the set of credentials and permissions the agent works with when it acts on your behalf — querying AWS, reaching a Kubernetes cluster, or calling an MCP server's tools.

![Scopes dropdown](../../.gitbook/assets/ticket-v2-step-04-scopes-dropdown.png)

Selected scopes appear in place of the **Select Scopes** button.

![Scope selected](../../.gitbook/assets/ticket-v2-step-05-scope-selected.png)

{% hint style="info" %}
Scope selection is optional. A ticket created without a scope can still plan, answer questions, and reason about your setup — it just has no credentials to act with. Add a scope when the agent needs to reach real infrastructure.
{% endhint %}

---

## Step 4 — Review the agent loadout

The **Agent loadout** row summarises how this ticket is configured — permissions, memory, and personas — and expands into three cards.

![Agent loadout](../../.gitbook/assets/ticket-v2-step-06-agent-loadout.png)

### Commands

Shows whether this ticket uses the workspace's default command permissions or its own rules. Click **Edit permissions** to set per-ticket rules.

![Command Execution Permission Settings](../../.gitbook/assets/ticket-v2-step-07-command-permissions-modal.png)

In the dialog you can:

- **Approve All** — allow every command the agent wants to run
- **Reject All** — deny all command execution
- **Add pattern for auto-approval** — any command matching the pattern runs without asking
- **Add pattern for auto-rejection** — any command matching the pattern is always blocked

MCP tool calls have their own equivalent settings, available from the ticket's Details panel once it exists — see [MCP Servers](mcp-servers/README.md#controlling-which-tools-the-agent-may-call).

### Agent context

Personas decide what the agent knows how to do. Add individual skills on top when a persona doesn't already cover them.

![Agent context](../../.gitbook/assets/ticket-v2-step-08-agent-context-modal.png)

### Workspace memory

When enabled, the agent reuses what earlier tickets in this workspace established — naming conventions, past runbooks, known-flaky nodes. **Memory is on by default**; switch it off for a one-off ticket where you don't want that context pulled in.

![Workspace memory card](../../.gitbook/assets/ticket-v2-step-09-workspace-memory-card.png)

See [Agent Memories](agents/agent-memories.md) for how memories are written and maintained.

---

## Step 5 — Describe the task and submit

Type what the agent should do in plain language, then click the arrow to submit.

![Task description entered](../../.gitbook/assets/ticket-v2-step-10-prompt-entered.png)

The system creates the ticket and opens it.

![Ticket created](../../.gitbook/assets/ticket-v2-step-11-ticket-created.png)

---

## The ticket page

The conversation with the agent runs down the left. On the right, three tabs — **Details**, **Files**, and **Activity** — hold the ticket's metadata, its files, and a comment thread.

![Ticket page with the Details panel](../../.gitbook/assets/ticket-v2-step-12-ticket-details-panel.png)

### Details

| Field | What it shows |
|---|---|
| **Status** | Current state — `Open`, `In Progress`, `Resolved`, or `Closed` |
| **LLM** | The model handling this ticket |
| **Total Cost** | Cumulative token cost consumed so far |
| **Ticket Summary** | A generated summary of the conversation |
| **Scopes** | The credential scopes attached; editable after creation |
| **Personas** | The persona modules active for this ticket; editable after creation |
| **Priority** | `Low`, `Medium`, `High`, or `Critical` |
| **Ticket ID** | Unique identifier, e.g. `aifullinternal-308` — use it to reference the ticket elsewhere |
| **Command Permissions** | Per-ticket command execution rules (same dialog as Step 4) |
| **MCP Tool Permissions** | Per-ticket MCP tool approval — see [MCP Servers](mcp-servers/README.md#controlling-which-tools-the-agent-may-call) |
| **Workspace Memory** | Toggle memory for this ticket on or off |
| **Ticket Secret** | A token external systems and webhooks can use to authenticate callbacks scoped to this ticket |
| **Context Files** | Attach manifests, CI configs, or logs for the agent to read as extra context |
| **Reports** | Structured outputs the agent produced — audit summaries, cost breakdowns, diagnostics |
| **Feedback List** | Rate and comment on the agent's responses; visible to administrators for quality review |

### Files

Files the agent created or read during the ticket.

![Files tab](../../.gitbook/assets/ticket-v2-step-13-tab-files.png)

### Activity

A comment thread on the ticket, separate from the agent conversation — use it to leave notes for colleagues working the same ticket.

![Activity tab](../../.gitbook/assets/ticket-v2-step-14-tab-activity.png)

---

## Approving commands as the agent works

When the agent wants to run a command that isn't covered by an auto-approval rule, it pauses and asks. The proposed command is shown in full, with **Approve**, **Reject**, and **Ignore**, plus a **Remember for this ticket** option that turns your choice into a rule for the rest of the conversation.

This is the default behaviour — the agent asks before running anything it hasn't been pre-authorised for.

---

## Live File Diffs

When the agent creates, edits, or overwrites a file, the change appears in the conversation as a diff instead of only a closing summary. The header shows whether the file was **created**, **edited**, or **overwritten**, along with `+N`/`-N` line-count badges — expand it to see the full line-by-line diff, with additions and deletions color-coded like a code review.

The diff appears once the file operation finishes — after the "Running tool" status, alongside the agent's usual explanation of what it changed and why — rather than streaming line-by-line as it's written.

---

## Long Conversations and Context Compaction

Long-running conversations are automatically compacted as they approach the underlying model's context window limit. The agent summarizes the earlier turns of the conversation and continues from that summary, rather than losing history or failing outright once the limit is reached.

While compaction is running, two things change in the ticket view:

* The conversation shows a status line — *"Compacting conversation history to fit the context window…"* — followed shortly by *"Compaction complete."* Click the completed line to expand it and see an excerpt of the summary the agent generated.
* The chat input's placeholder changes to *"Compacting conversation history…"*, and the **Stop** button is disabled with the tooltip *"Compacting — cannot stop."*

Compaction is fully automatic — there is no setting to configure or threshold to tune. It is triggered by the underlying model's context window, not by a DuploCloud-side limit.

{% hint style="info" %}
This is distinct from **Ticket Summary** in the Details panel, which produces a one-off, manually-triggered summary. Compaction happens automatically mid-conversation to keep the agent within its context limits — the two features are unrelated.
{% endhint %}

---

## Playwright Test

```
tests/ticket-create-reshoot.spec.ts
```

```bash
npx playwright test ticket-create-reshoot.spec.ts --project=chromium --workers=1 --timeout=1200000
```
