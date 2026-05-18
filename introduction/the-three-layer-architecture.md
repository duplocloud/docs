---
description: 'From Automation to Cognition: Architecting an AI-Native DevOps Platform'
---

# The Three-Layer Architecture

**The Three-Layer Architecture: ARMOR, Extensions, and Studio**

An extensible AI-native platform purpose-built for multiplayer enterprise Devops.

## Introduction

Chapter 1 identified twelve capabilities that enterprise DevOps demands from AI — multiplayer sessions, centralized context, RBAC, determinism, cost management, and more. It showed why three waves of AI tooling failed to deliver them, and why personalized and managed agents, while transformative for individuals, are architecturally single-player.

This chapter introduces the product that closes the gap. The Architecture is a three-layer architecture purpose-built for multiplayer enterprise operations.

### Three Layers. One Platform.

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><mark style="color:$warning;">LAYER 1 — ARMOR</mark><br><strong>Agent Runtime for Multiplayer Operations</strong> <br>The foundation. ARMOR implements all twelve enterprise requirements — ticketing (multi-user AI sessions), connectors (secure access to IT systems), intelligence (skills and business logic), centralized context (organizational memory), workspaces and RBAC, projects (spec-driven workflows), determinism, token less analytics, and cost management. Every interaction with AI happens inside a ticket.</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><mark style="color:$warning;">LAYER 2 — EXTENSION FRAMEWORK</mark></p><p><strong>Custom Automation Workflows</strong> <br>Build your own custom workflows based on specific business needs. Define a resource taxonomy (Network → Cluster → Environment → Workloads). Write skills for each resource type. The framework generates forms, REST APIs, list views, status tracking, dependency enforcement. All ARMOR capabilities are inherited automatically. DuploCloud comes with a default DevOps extension that includes everything from Deployment, Security, Observability to CI-CD. Multiple compliance standards are implemented out-of-box.</p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><mark style="color:$warning;">LAYER 3 — STUDIO</mark></p><p><strong>Developer Experience &#x26; Hosting</strong> </p><p>Imagine Replit for DevOps. With DuploCloud Studio Operators can build and deploy their automation platform in hours. Open a web interface or launch Claude Code with the DuploCloud plugin. Define your policy model, write skills, connect providers, configure workspaces, onboard users. Hosted by DuploCloud or self-hosted on your own Kubernetes infrastructure.</p></td></tr></tbody></table>

This chapter focuses on <mark style="color:$warning;">**ARMOR**</mark> — the foundational runtime that makes everything above it possible. Extensions and Studio are covered in subsequent chapters.

![](<../.gitbook/assets/image copy.png>)

## Architecture Overview

ARMOR is built on a simple principle: **every interaction with AI happens inside a ticket**. The ticket is the unit of work, the audit trail, the collaboration surface, and the cost boundary. Everything else — connectors, skills, workspaces, projects, analytics — exists to feed context into tickets and consume results from them.

**The ARMOR Backend** — a single deployable service containing the ticketing system, all functional modules (connectors, intelligence, context, projects, analytics, cost management), workspace management, and RBAC. Users interact through a web browser, REST API, Claude Code plugin, or Slack/Teams.

**The ARMOR Agent** — a separate service built on the Agent SDK from the LLM Vendors like Claude, OpenAI and Gemini. For other models we use OpenCode.. It receives work from the ticketing system as questions, credentials, and input context. It returns answers and output context. The agent operates on IT systems directly and reads/writes to a shared file system for context exchange.

**The LLM** — foundational models called by the agent for reasoning, planning, and execution.

### The Ticketing System — Foundation

The ticketing system is the heart of the ARMOR architecture. Every interaction with AI — whether it’s a one-off question, a step in a complex project, a dashboard creation, or a resource provisioning operation — happens inside a ticket. A ticket is not just a chat thread. It is a multi-user AI session with the following properties:

| <p><strong>Multiplayer by Default</strong> </p><p>Multiple users access the same ticket. The morning engineer picks up with full context, reasoning history, and system state from the 2 AM on-call.</p> | <p><strong>Complete Context</strong> </p><p>Each ticket has its own context folder on a shared file system. The backend keeps it current — all user data and output artifacts stored there.</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Complete Audit Trail</strong> </p><p>Every action, tool call, and decision recorded. A system of record for compliance review, not just a conversation log.<br></p>                           | <p><strong>Scoped Execution</strong> </p><p>Each ticket operates within a defined scope — the IT systems, credentials, and permissions the agent can use. The system enforces boundaries.</p>   |
| <p><strong>Cost-Tracked</strong> </p><p>Every ticket records token consumption at every chat turn. Full visibility into what each piece of work cost, by ticket, user, and workspace.</p>                | <p><strong>Human-in-the-Loop Safety</strong> </p><p>No command executes without explicit user approval. Customizable with auto-approvals, blacklists, and whitelists per ticket.<br></p>        |

> Because the ticket is the universal unit of work, every other module integrates through it. Projects create tickets. Dashboards are created through tickets. Resource provisioning triggers tickets. Audit trails, cost tracking, RBAC, and multiplayer collaboration apply to **everything** — without building these capabilities separately for each feature.

### **Connectors — Secure Access to IT Systems**

Connectors are how the platform reaches the outside world. They consist of three concepts:

| <p><strong>Providers</strong> </p><p>Any IT system — AWS, Azure, GCP, Kubernetes, GitHub, Datadog, PagerDuty, ServiceNow, or any system accessible via MCP servers.<br><br></p> | <p><strong>Credentials</strong> </p><p>API keys, service account tokens, certificates. Stored securely, never exposed to users. Users select scopes, never handle credentials.<br><br></p> | <p><strong>Scopes</strong> </p><p>Provider + credential + granular access controls (regions, namespaces, resource types). Reusable across workspaces. What users select when creating a ticket.</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

This three-tier model solves the credential safeguarding problem. The agent operates with enterprise credentials, but those credentials flow through the system without ever being visible in a conversation, a prompt, or an AI response.

### Intelligence — Skills and Business Logic

In traditional DevOps SaaS, business logic is hardcoded by the vendor. In ARMOR, business logic is expressed as Skills — instructions that tell the agent how to behave and what capabilities it has.

> Skills implement two main functionalities: **customizing business logic** and **adding determinism**. Instead of waiting for a vendor to code a new workflow, any team member with domain expertise can write a Skill. Skills containing custom scripts provide the determinism layer, backed by ticket safety controls.

A Skill is a folder containing a SKILL.md file with metadata, instructions, and optionally scripts, templates, and reference materials. There are three types:

| <p><strong>Platform Skills</strong> <br>Pre-built capabilities shipping with the platform. Baseline troubleshooting, dashboard creation, project management.</p> | <p><strong>External Skills</strong> <br>Third-party packages from vendors like Pulumi, HashiCorp, or cloud providers.<br></p> | <p><strong>Custom Skills</strong> <br>Created by the customer’s team. Encode your organization’s specific workflows, policies, and operational practices.</p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Business logic is **user-owned and user-modifiable**. An organization can fork a platform skill and customize it — adding their own tagging policies, compliance requirements, or architectural standards — without waiting for a vendor update.

#### Personas

A Persona bundles related Skills by role or function. An SRE Persona might combine troubleshooting, monitoring, and incident response skills. A Provisioning Persona could bundle Terraform and Kubernetes deployment skills. Personas can include system prompts that shape the agent’s overall behavior. In a ticket, users select a persona instead of individual skills.

### Central Context — Organizational Memory

Desktop agents suffer from context amnesia — when a session ends, everything the agent learned disappears. In ARMOR, all context is centralized. Every ticket’s inputs, outputs, reasoning chains, and artifacts are stored in a shared file system accessible to the workspace.

| <p><strong>Context Persists Across Sessions</strong> <br>When one engineer diagnoses a DNS misconfiguration on Monday, the resolution is part of workspace context. Another engineer encountering a similar issue Thursday already has the history.<br></p> | <p><strong>Context Compounds Over Time</strong> <br>Every ticket adds to the workspace’s knowledge base. Reports, artifacts, configs, and decision logs accumulate. The workspace gets smarter with use.<br><br></p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Context is workspace-scoped. One team’s operational history doesn’t leak into another team’s workspace. Organizational separation is preserved.

### Workspaces and RBAC

The Workspace is the organizational container that binds **scopes** (which IT systems are available), **personas** (which skills the agent has), **users** (who can access it), and **context** (accumulated files and outputs). Tickets, projects, dashboards, and resources all live within a workspace.

Create multiple workspaces — one per team, per environment, per business unit. An L1 SRE workspace might have read-only access to infrastructure with an SRE Persona. A Platform Engineering workspace might have full write access with a Provisioning Persona.

All access control is built around workspaces. RBAC governs which users access which workspaces, and which scopes they use within each. Every AI action is traceable to a specific user, within a specific workspace, using a specific scope — providing the auditability that SOC 2, HIPAA, and PCI-DSS require.

### Projects — Spec-Driven Workflows

Complex, multi-step initiatives — migrating infrastructure, setting up a new environment, implementing a compliance framework — need structure. Projects provide it:

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><strong>Spec → Plan → Tasks → Tickets</strong><br><strong>Spec:</strong> User provides high-level requirements. Agent collaborates to produce a detailed specification. Reviewed and approved before work begins.<br><strong>Plan:</strong> Agent generates a step-by-step implementation plan. Tasks organized into stages — parallel within a stage, sequential across stages.<br><strong>Tasks:</strong>Each task becomes a ticket. Concurrent execution within stages for speed, sequential stages for predictability. The AI does the work; the human owns the decisions.</td></tr></tbody></table>

### Token less Analytics

Fifty engineers checking the same deployment status dashboard means fifty inference cycles for identical information. ARMOR implements tokenless analytics: dashboards are created through tickets, but they run without AI.

When a user asks for a dashboard, the agent designs it — understanding data sources, generating query logic, building visualization scripts. These artifacts are saved. From that point forward, refreshing executes only the scripts, pulling data from source systems without a single LLM call.

> _AI should create the dashboard. It shouldn’t run the dashboard. The intelligence is in the design, not in the rendering._

### Cost Management

Token cost is the single biggest blocker to enterprise AI adoption. ARMOR treats cost management as a first-class architectural concern:

| <p><strong>Per-Ticket Tracking</strong> </p><p>Every ticket records token consumption at every chat turn. Full visibility by ticket, user, and workspace.<br></p> | <p><strong>Quotas</strong> <br>Token quotas at workspace, project, and ticket levels. Production SRE gets higher quotas than dev sandbox. Warnings before limits.</p> | <p><strong>Usage Analytics</strong> <br>Cost data aggregated across workspaces, teams, and time periods for planning, budgeting, and optimizing AI spend.</p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### The ARMOR Agent

The ARMOR Agent is a separate service built on the **Claude SDK** — internally running the same Claude CLI that runs in Claude Code on your desktop. When the ticketing system dispatches a ticket, the agent receives the question, credentials, and input context. It returns the answer and output context.

The agent is intentionally thin. No domain tools or vertical logic — that belongs in Skills. The agent implements the plumbing that makes an LLM SDK safe, multi-tenant, and enterprise-grade:

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>1</strong></td><td><p><strong>Session Isolation</strong></p><p>Every ticket gets its own working directory. No read or write can cross from one ticket’s directory to another’s.</p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="42.29296875"></th><th></th></tr></thead><tbody><tr><td><strong>2</strong></td><td><strong>Credential Translation</strong><br>Backend passes credentials as structured data. Agent translates to kubeconfig, AWS credential files, GCP application default credentials. LLM never sees raw credentials.</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>3</strong></td><td><strong>Skill Provisioning</strong><br>Skills live on the shared file system, versioned by the backend. Agent maps assigned skills into the session directory before execution.</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>4</strong></td><td><strong>MCP Server Configuration</strong><br>External capabilities surfaced via MCP servers. Agent writes configuration before execution begins.</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>5</strong></td><td><strong>Sandboxing</strong><br>All shell execution in a sandbox. File system constrained to the ticket’s scope. Boundary enforced at the OS level, not the prompt level.</td></tr></tbody></table>

{% hint style="info" %}
We don’t build agents for individual use cases — we use the agent SDKs published by LLM vendors. **This has been the single biggest factor in our feature velocity.** We have one version of the ARMOR agent for each of Claude, OpenAI, and Gemini. For all other models, a version based on Open Code.
{% endhint %}

#### What’s Next

ARMOR is the foundation — the multiplayer agent runtime that delivers all enterprise capabilities. But the power of the platform is in what gets built on top of it.
