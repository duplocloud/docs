# Create a Ticket Tutorial

This document explains how to create a new ticket in the DuploCloud AI Suite HelpDesk, configure the agent, scope, and skills, and interact with the AI agent on the resulting ticket page.

---

## Prerequisites

- Access to the DuploCloud AI Suite
- An authenticated user account
- At least one agent, scope, and skill configured in the system

---

## Step 1 — Navigate to Add Ticket

Go to **HelpDesk** in the left-hand navigation and click **Add Ticket**, or navigate directly to the add ticket URL. The **Create a new ticket** form appears with fields for Select Agent, Select Scopes, and Advanced Options.

![Step 1 — Add Ticket page](../../.gitbook/assets/step-01-add-ticket-page.png)

---

## Step 2 — Select an Agent

Click the **Select Agent** button. A dropdown list appears showing all available AI agents. The option to select is highlighted below.

![Step 2 — Agent dropdown with generic-agent highlighted](../../.gitbook/assets/step-02-agent-dropdown.png)

Click **generic-agent** to select it.

![Step 3 — generic-agent selected](../../.gitbook/assets/step-03-agent-selected.png)

The **agent** determines which AI model handles your ticket. Different agents may have different specializations, tools, and capabilities.

---

## Step 3 — Select a Scope

Click the **Select Scopes** button. A dropdown appears showing all scopes your account has access to. The option to select is highlighted below.

![Step 4 — Scope dropdown with full-admin-token highlighted](../../.gitbook/assets/step-04-scope-dropdown.png)

Click **full-admin-token** to select it.

![Step 5 — full-admin-token selected](../../.gitbook/assets/step-05-scope-selected.png)

A **scope** defines the set of credentials and permissions the agent will use when executing actions on your behalf (e.g., querying AWS, accessing Kubernetes clusters, calling APIs).

---

## Step 4 — Open Advanced Options

Click **Advanced Options** to expand the advanced configuration section, as highlighted below.

![Step 6 — Advanced Options expanded](../../.gitbook/assets/step-06-advanced-options.png)

This reveals two additional settings: **Personas** and **Non Interactive**.

---

## Step 5 — Select All Personas

In the **Personas** section check all personas you want the agent to use. The personas selection is highlighted below.

![Step 7 — Personas section highlighted](../../.gitbook/assets/step-07-skills-selected.png)

**Personas** control which specialized knowledge modules the agent can invoke. For example, the `devops` persona enables CI/CD and Kubernetes guidance, while `GCP-troubleshooting` enables GCP-specific diagnostics.

---

## Step 6 — Non Interactive Option (Optional)

The **Non Interactive** option is highlighted below. Leave it **unchecked** for a standard interactive session.

![Step 8 — Non Interactive option highlighted](../../.gitbook/assets/step-08-non-interactive.png)

> **Note:** Enabling **Non Interactive** causes the agent to run autonomously end-to-end without pausing for user input. Useful for fully automated workflows — leave unchecked for normal conversational use.

---

## Step 7 — Enter Your Question

Click in the text area and type your question or task description. The textarea is highlighted below.

![Step 9 — Question textarea highlighted](../../.gitbook/assets/step-09-question-entered.png)

---

## Step 8 — Submit: Create Ticket

Click the **Create Ticket** button, highlighted below, to submit the form.

![Step 10 — Create Ticket button highlighted](../../.gitbook/assets/step-10-create-ticket-button.png)

The system processes the request and redirects you to the ticket detail page.

![Step 11 — Ticket page after creation](../../.gitbook/assets/step-11-ticket-page.png)

---

## Ticket Page — Feature Overview

After creating a ticket you land on the ticket detail page. The page has an **Activity Feed** on the left for the conversation with the agent, and a **Ticket Details** sidebar on the right showing metadata.

---

### Ticket Details

The **Ticket Details** heading (highlighted) marks the start of the sidebar that summarises all ticket metadata.

![Ticket Details heading highlighted](../../.gitbook/assets/step-12-ticket-details.png)

---

### Status

The **STATUS** field (highlighted) shows the current state of the ticket — `Open`, `In Progress`, `Resolved`, or `Closed`.

![STATUS field highlighted](../../.gitbook/assets/step-13-status.png)

---

### Total Cost

The **TOTAL COST** field (highlighted) shows the cumulative token/compute cost consumed by the AI agent for this ticket.

![TOTAL COST field highlighted](../../.gitbook/assets/step-14-total-cost.png)

---

### Scopes

The **SCOPES** field (highlighted) lists the credential scope(s) attached to this ticket (e.g., `full-admin-token`). The agent uses these credentials when executing actions on your behalf.

![SCOPES field highlighted](../../.gitbook/assets/step-15-scopes.png)

---

### Personas

The **PERSONAS** field (highlighted) lists the persona modules active for this ticket (e.g., `devops`, `GCP-troubleshooting`, `GCP-IAC`). These control which specialized knowledge the agent can draw upon.

![PERSONAS field highlighted](../../.gitbook/assets/step-16-personas.png)

---

### Priority

The **PRIORITY** field (highlighted) indicates the urgency level of the ticket — `Low`, `Medium`, `High`, or `Critical`.

![PRIORITY field highlighted](../../.gitbook/assets/step-17-priority.png)

---

### Ticket ID

The **TICKET ID** field (highlighted) is the unique identifier for the ticket in the format `<WORKSPACE>-<NUMBER>` (e.g., `AIFULLINTERNAL-45`). Use this ID to reference the ticket in logs, reports, or support conversations.

![TICKET ID field highlighted](../../.gitbook/assets/step-18-ticket-id.png)

---

### Ticket Secret

The **Ticket Secret** section (highlighted) displays a secret token associated with this ticket. This token can be used by external systems or webhooks to authenticate callbacks and API calls scoped to this specific ticket.

![Ticket Secret section highlighted](../../.gitbook/assets/step-19-ticket-secret.png)

---

### Command Permissions

The **Command Permissions** section (highlighted) controls what system commands the agent is allowed to execute during this ticket.

![Command Permissions section highlighted](../../.gitbook/assets/step-20-cmd-perms-section.png)

Clicking it opens the **Command Execution Permission Settings** modal shown below.

![Command Permissions modal](../../.gitbook/assets/step-21-cmd-perms-modal.png)

Inside the modal you can:
- **Approve All** — allow all commands the agent wants to run
- **Reject All** — deny all command execution
- **Add pattern for auto-approval** — any command matching the pattern is automatically approved
- **Add pattern for auto-rejection** — any command matching the pattern is always blocked

---

### Context Files

The **Context Files** section (highlighted) allows you to attach files such as Kubernetes manifests, CI configs, or logs. The agent reads these as additional context when answering your question or executing tasks.

![Context Files section highlighted](../../.gitbook/assets/step-22-context-files.png)

---

### Reports

The **Reports** section (highlighted) shows any structured reports or outputs generated by the agent during this ticket, such as audit summaries, cost breakdowns, or diagnostic results.

![Reports section highlighted](../../.gitbook/assets/step-23-reports.png)

---

### Feedback List

The **Feedback List** section (highlighted) lets you rate and comment on the agent's responses. Feedback is logged and visible to administrators for quality review and model improvement.

![Feedback List section highlighted](../../.gitbook/assets/step-24-feedback-list.png)

---

### Activity Feed

The **Activity Feed** on the left is where the conversation with the agent takes place. Your original question appears at the top, and the agent streams its response below it in real time.

![Activity feed with agent response](../../.gitbook/assets/step-25-activity-feed.png)

---

## Playwright Test

```
tests/ticket-create.spec.ts
```

```bash
npx playwright test ticket-create.spec.ts --project=chromium --timeout=300000
```
