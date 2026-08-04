# Product Updates

## June–July 2026

---

**1.** `Feature` — [**HelpDesk Audit Trail**](../armor/helpdesk/audit-trail.md)

All HelpDesk activity is now captured in a pluggable, configurable audit log.
- Audit sinks support S3, local file, and console output
- Sensitive fields are automatically masked in audit records
- Captures auth failures (401/403/404/405) and always logs even when an action throws

Changes in: `Backend`

---

**2.** `Feature` — [**User-Level Cloud Credentials**](../armor/providers/user-level-credentials.md)

Individual users can now hold their own scoped cloud credentials rather than sharing team-level credentials, including secure materialization into agent sandboxes.

Changes in: `Agent` `Backend` `Frontend`

---

**3.** `Feature` — [**Azure AD & Okta User Sync**](../armor/access-control/azure-ad-okta-user-sync.md)

User accounts can now be synced in from Azure AD or Okta instead of manual provisioning.

Changes in: `Backend` `Frontend`

---

**4.** `Feature` — [**LLM Model Registry & Configurable Model Mapping**](../armor/agents/llm-models.md)

Model access is now governed by a central registry with an allow-list and resolution order (Project → Workspace → Platform), including SDK-aware pairing and first-deploy seeding.
- User-configurable model selection in AI Studio
- GCP Vertex model seeding alongside existing providers

Changes in: `Backend` `Frontend`

---

**5.** `Feature` — [**GCP Vertex AI Support**](../armor/agents/gcp-vertex-ai-support.md)

The agent runtime can now run against GCP Vertex AI in addition to existing providers, with GCP partner attribution wired through the CLI/SDK calls.

Changes in: `Agent` `Backend`

---

**6.** `Feature` — [**Platform Analytics Dashboard & Observability**](../armor/analytics.md)

A comprehensive analytics dashboard was added to AI Studio, backed by LangFuse tracing in the agent runtime.
- Observability iframe with LangFuse configuration and a settings deep-link
- Agent traces enriched with helpdesk/ticket context
- User last-login tracking on auth endpoints

Changes in: `Agent` `Backend` `Frontend`

---

**7.** `Feature` — [**Command Policy Admin**](../armor/access-control/command-policy.md)

Admins can now define command policies that are enforced during chat/ticket execution.

Changes in: `Backend` `Frontend`

---

**8.** `Feature` — [**Slash-Command Skill Picker**](../armor/skills/README.md#referencing-a-skill-with-the-slash-picker)

Users can now browse and invoke skills via a "/" command picker in chat and ticket creation, including interactive skill browsing.

Changes in: `Agent` `Frontend`

---

**9.** `Feature` — [**Workspace Memory Management**](../armor/agents/agent-memories.md)

Agent memory is now configurable per workspace and per ticket.
- Admin page to view, edit, add, and delete agent memory files
- Per-ticket opt-out toggle for workspace memory
- Config precedence resolver (project/workspace > env > system)

Changes in: `Agent` `Backend` `Frontend`

---

**10.** `Feature` — [**Human-in-the-Loop Approval for MCP Tool Calls**](../armor/access-control/ai-guardrails.md#mcp-tool-call-approval)

External MCP tool calls now route through a user approval gate before executing, with durable approval UI that survives across turns.
- Approval/result UI surfaced directly in chat
- Silent approve/reject decisions honored without re-prompting
- Pending approvals can time out gracefully without losing turn context

Changes in: `Agent` `Frontend`

---

**11.** `Feature` — [**Portal Notification Providers (incl. SMTP)**](../armor/additional-components/notifications.md)

Admins can now configure notification providers, including SMTP, and manage portal notification settings.

Changes in: `Backend` `Frontend`

---

**12.** `Feature` — [**AI Suite System Settings & Global Secrets**](../armor/settings.md)

A new admin surface for platform- and workspace-scoped system settings, plus a global, platform-wide secrets scope.

Changes in: `Backend` `Frontend`

---

**13.** `Feature` — **Configurable UI Theming**

AI Studio's look can now be customized via CSS custom properties instead of a fixed theme.

Changes in: `Frontend`

---

**14.** `Feature` — **Group Chat Mode for Multi-Party Conversations**

The agent's group-chat handling was generalized to all multi-party origins (e.g. Slack channels, Teams groups), not just direct messages.

Changes in: `Agent`

---

**15.** `Feature` — **Slack Message Batching & Silence Detection**

The agent now batches related Slack messages and detects conversational silence to respond more naturally instead of reacting to every message individually.

Changes in: `Agent`

---

**16.** `Feature` — [**Workspace-Level Custom Instructions**](../armor/workspaces.md#setting-a-system-prompt)

Workspaces can now define custom instructions that are injected into the agent's system prompt, distinct from persisted workspace memory files.

Changes in: `Agent`

---

**17.** `Feature` — [**Project-Level Context for Tickets**](../armor/projects.md)

Tickets can now carry Project-level context in addition to Workspace, giving agents access to project-scoped configuration alongside workspace and platform settings.

Changes in: `Agent` `Backend`

---

**18.** `Enhancement` — **Security Hardening — Auth, Access & Data**

A broad round of security improvements across the platform.
- JWT tokens are now revoked on logout, role change, and account deactivation
- OAuth redirect URIs are validated against an allow-list to prevent open-redirect/token exfiltration
- Fixed a cross-tenant IDOR issue on resource metadata and user credentials, and sanitized ticket title/description HTML input
- Credential secrets are now masked in admin read paths and the Edit Credential dialog

Changes in: `Agent` `Backend` `Frontend`

---

**19.** `Enhancement` — **Agent Runtime Hardening & Reliability**

The agent execution sandbox and runtime got a reliability and security pass.
- Agent now runs as a non-root user (uid 1001) in a capless sandbox
- New /health/inflight endpoint enables graceful draining during rolling deploys
- New /version endpoint exposes build provenance

Changes in: `Agent` `Backend`

---

**20.** `Feature` — **Terraform-Managed Environments (Infrastructure as Code)**

Environments can now be defined, planned, and applied as Terraform modules directly from the platform, with git-diff visibility before changes go live.
- Full TfDeployment/TfEnvironment/TfState lifecycle with independent plan and apply flows
- Live git-diff view of pending infrastructure changes before applying
- Multi-provider support, including the DuploCloud Terraform provider and GitLab

Changes in: `Backend` `Frontend`

---

**21.** `Feature` — **AWS Just-in-Time (JIT) Access for Resource Groups**

Users can now obtain temporary, scoped AWS access tied to a Resource Group instead of standing credentials.
- Assume-role and federation-URL primitives scoped to the resource group
- Read-only access enforcement option
- Chained credentials support for nested scopes

Changes in: `Backend` `Frontend`

---

**22.** `Feature` — **AWS EFS Support**

Elastic File System is now a manageable resource type within environments.

Changes in: `Backend` `Frontend`

---

**23.** `Feature` — **AWS MSK (Kafka) Support**

Managed Streaming for Kafka clusters can now be provisioned and managed from the platform.

Changes in: `Backend` `Frontend`

---

**24.** `Feature` — **AWS SQS Queue Management**

SQS queues are now a fully manageable resource, including encryption configuration.

Changes in: `Backend` `Frontend`

---

**25.** `Feature` — **AWS SNS Topic Management**

SNS topics can now be created and managed directly from the platform.

Changes in: `Backend` `Frontend`

---

**26.** `Feature` — **AWS EventBridge Rule Management**

EventBridge rules and their targets are now manageable, with targets handled through dedicated endpoints rather than being tied to the rule record.

Changes in: `Backend` `Frontend`

---

**27.** `Feature` — **AWS ECR Repository Support**

ECR repositories are now a manageable resource under Storage.

Changes in: `Backend` `Frontend`

---

**28.** `Feature` — **AWS SSM Parameter Store Support**

SSM Parameters, including SecureString values, can now be created and managed from the platform.

Changes in: `Backend` `Frontend`

---

**29.** `Feature` — **Expanded RDS Management**

RDS instances and clusters gained several operational capabilities.
- On-demand snapshot creation with a dedicated Snapshots tab (instance and cluster)
- Storage autoscaling, Secrets Manager integration, and CloudWatch log exports
- IOPS configuration support for io1/io2/gp3 storage types

Changes in: `Backend` `Frontend`

---

**30.** `Feature` — **Kubernetes Ingress Support**

Kubernetes Ingress resources, including ingress groups, are now manageable from the platform.

Changes in: `Backend` `Frontend`

---

**31.** `Feature` — **EC2 Hosts as a Managed Resource**

EC2 hosts can now be added, viewed, and managed as environment resources.

Changes in: `Backend` `Frontend`

---

**32.** `Feature` — **Kubernetes Horizontal Pod Autoscaler (HPA) Management**

HPA resources can now be created and managed directly from the UI, with validation for External HPA resource requests.

Changes in: `Frontend`

---

**33.** `Feature` — **Imported (Existing) Cluster Support**

Customers can now bring an existing Kubernetes cluster into the platform rather than only provisioning new ones.

Changes in: `Backend` `Frontend`

---

**34.** `Feature` — **Azure Kubernetes Cluster Support**

Azure-hosted Kubernetes clusters are now supported alongside AWS.

Changes in: `Backend` `Frontend`

---

**35.** `Feature` — **AWS S3 Bucket Management**

S3 buckets are now a manageable resource type, including region selection at creation time.

Changes in: `Backend` `Frontend`

---

**36.** `Feature` — **AWS Lambda Enhancements (Layers, DLQ, Runtime Config)**

Lambda function management was extended with layers, dead-letter queue configuration, and additional runtime endpoints.

Changes in: `Backend` `Frontend`

---

**37.** `Feature` — **Cloud Resource Groups Without a Kubernetes Cluster**

Cloud-based Resource Groups no longer require a Kubernetes cluster, letting customers use cloud-only resources without provisioning K8s.

Changes in: `Backend` `Frontend`

---

**38.** `Feature` — **Customer-Managed KMS Key (CMK) Support**

Customer-managed KMS keys are now supported and validated across cluster and RDS resource creation.
- CMK support for secondary clusters
- KMS key field now conditionally shown based on RDS storage encryption settings
- Centralized KMS key validation patterns across forms

Changes in: `Backend` `Frontend`

---

**39.** `Feature` — **PVC (Persistent Volume Claim) Management**

Persistent Volume Claims gained edit support and better status visibility.
- PVCs can now be edited directly in AI Studio
- Storage size validation on PVC forms
- PVC badge now reflects live Kubernetes phase instead of DuploCloud's cached status

Changes in: `Backend` `Frontend`

---

## May 2026

---

**1.** `Feature` — [**LLM Cost & Usage Quota Controls**](../armor/access-control/quotas.md)

A full quota enforcement system now governs LLM/agent usage costs, checked before every LLM call.
- Six enforcement cases: workspace, per-user, per-ticket, and platform-wide caps with configurable defaults
- Per-turn usage recording for auditing and reporting
- Quotas can now map to multiple workspaces at once, with an admin UI for configuring and viewing limits

Changes in: `Backend` `Frontend`

---

**2.** `Feature` — [**Direct Anthropic API Support**](../armor/agents/direct-anthropic-api-support.md)

The agent can now call the Anthropic API directly as a model provider, alongside existing Bedrock/Vertex routes.

Changes in: `Agent`

---

**3.** `Feature` — [**AWS Bedrock Guardrails Support**](../armor/access-control/ai-guardrails.md#aws-bedrock-guardrails)

Bedrock-backed agent runs can now be configured with AWS Bedrock Guardrails for content/safety filtering.

Changes in: `Agent`

---

**4.** `Feature` — [**Context Compaction for Long-Running Conversations**](../armor/tickets.md#long-conversations-and-context-compaction)

Long conversations are now automatically compacted to stay within context limits, with live status feedback in chat.
- Automatic detection of when a conversation needs compaction
- Streaming status updates while compaction runs
- Chat UI shows status and disables controls during compaction

Changes in: `Agent` `Frontend`

---

**5.** `Feature` — **Workspace-Level Auto-Memory (initial release)**

Workspaces can now automatically persist agent memory by default — the foundation for the later Workspace Memory admin tooling shipped in July.

Changes in: `Agent`

---

**6.** `Feature` — [**MCP Server Credential References**](../armor/mcp-servers/credential-masking-for-mcp-servers.md)

MCP servers can now be configured with credential placeholders/references instead of hardcoded values.

Changes in: `Agent`

---

**7.** `Feature` — [**Live File Diff Streaming**](../armor/tickets.md#live-file-diffs)

When the agent writes or edits a file, a live diff now streams to chat instead of only a final summary.

Changes in: `Agent`

---

**8.** `Feature` — [**Prompt Suggestions & Templates for Workspaces**](../armor/agents/README.md#prompt-suggestions-and-templates-on-the-ticket-screen)

Admins can now configure suggested prompts and templates at the workspace level to guide ticket creation.

Changes in: `Frontend`

---

**9.** `Feature` — [**Shareable Links for Analytics Reports**](../armor/additional-components/reports.md#sharing-a-report)

Reports in Analytics > Reports can now be shared via a direct link that opens straight to the report's preview, instead of the recipient having to navigate and search for it manually. The recipient still needs to be logged in with access to the workspace the report belongs to — this is an in-app deep link, not a public link.

Changes in: `Frontend`

---

**10.** `Feature` — **Network Baseline v2**

Network Baseline (compliance network-configuration snapshots) was reworked into a v2 model across backend and UI.

Changes in: `Backend` `Frontend`

---

**11.** `Feature` — **AWS Lambda Support (initial)**

Lambda functions became a manageable resource type this month — later extended with layers/DLQ/runtime config in July.

Changes in: `Backend` `Frontend`

---

**12.** `Feature` — **AWS S3 Tables Support**

AWS S3 Tables are now a supported, inventoried resource with console access.

Changes in: `Frontend`

---

**13.** `Feature` — **AWS Glue UI Support**

AWS Glue jobs/connections are now manageable through the UI.

Changes in: `Frontend`

---

**14.** `Feature` — **RDS Blue/Green Deployment Support**

RDS Blue/Green deployments (zero-downtime major-version upgrades) are now visible and manageable in the UI.

Changes in: `Frontend`

---

## April 21–28, 2026

---

**1.** `Feature` — **MCP Raw Config Support**

Users can now provide a fully custom raw JSON MCP server configuration, unlocking support for any MCP server regardless of transport type.
- Supports HTTP, SSE, and Raw config types — selectable when adding or editing an MCP server
- Raw mode provides a JSON editor directly in the UI for pasting full server config
- Existing HTTP/SSE connections are unaffected

Changes in: `Backend` `Frontend` `Agent`

---

**2.** `Feature` — **GitLab CLI Integration**

The AI agent can now authenticate to GitLab and run `glab` commands, mirroring the existing GitHub integration.
- Supports both GitLab SaaS and self-managed instances
- Credentials are scoped per session and cleaned up automatically when the session ends
- Multiple GitLab hosts can be configured via workspace scopes

Changes in: `Agent`

---

**3.** `Feature` — **ASG Multiple Instance Types**

Auto Scaling Groups can now be configured with mixed instance policies for better cost and availability control.
- Choose multiple instance types or define requirements by vCPU and memory range
- Control the split between on-demand and spot capacity in the advanced settings
- Existing single-instance ASG configurations continue to work without changes

Changes in: `Frontend`

---

**4.** `Feature` — **Slack Integration Management for Tickets**

Service Desk tickets can now be linked to a Slack channel and thread directly from the ticket panel.
- View and update the Slack channel and thread associated with any ticket
- Copy a ready-made association command to link an existing Slack thread
- Connection status is visible at a glance from within the ticket management panel

Changes in: `Frontend`

---

**5.** `Feature` — **Agent Sandbox Enhancements**

Agents can now access workspace and project directories automatically, and run Python-based MCP servers out of the box.
- Workspace and project folders are mounted into the agent sandbox based on the platform context — no manual path configuration needed
- Python MCP servers using the `uvx` pattern (e.g. `uvx mcp-grafana`) are now supported
- The sandbox can be disabled via environment variable for deployments that require it

Changes in: `Agent`

---

## April 7–14, 2026

---

**1.** `Feature` — **Cross-Workspace Report Sharing**

Share AI reports with other workspaces directly from the report menu.
- Reports can be shared with one or more workspaces via a multi-select dialog; shared reports appear in recipient workspaces with a clear indicator
- Recipients can remove themselves without contacting the report owner

Changes in: `Backend` `Frontend`

---

**2.** `Feature` — **Workspace & Project Secrets Management**

Sensitive credentials can now be stored securely at the workspace, project, and ticket level.
- Secrets are encrypted at rest using AES-256
- UI provides dedicated modals for managing secrets across workspaces, projects, and service desk tickets

Changes in: `Backend` `Frontend`

---

**3.** `Feature` — **Dashboard Categories & Templates**

AI dashboards are now organized into categories with tabbed navigation and publish controls.
- Dashboards grouped under categories and navigated as tabs with configurable per-dashboard timeouts
- Templates support a publish/unpublish workflow; admins can promote templates as global
- Drag-and-drop support for dashboard organization, with YAML editing and link/investigation views

Changes in: `Backend` `Frontend`

---

**4.** `Feature` — **Provider Credential Encryption & Custom Fields**

Provider credentials are now encrypted at rest and support structured, typed custom field definitions.
- Supports arbitrary custom key-value fields with types: string, secret, certificate, and more
- UI provides a scrollable modal for managing structured credentials with inline editing

Changes in: `Backend` `Frontend`

---

**5.** `Feature` — **Private Git Repository Skills**

AI skills can now be loaded directly from private Git repositories.
- Skills support a new Private Git Repository format type with configurable org, repo, branch, and folder path
- Admin UI includes a Git repository configuration form within the Add/Edit skill workflow

Changes in: `Backend` `Frontend`

---

**6.** `Feature` — **Slack Integration**

The AI agent can now receive and respond to messages from Slack.
- Messages from Slack are processed with Slack-specific instructions
- The agent can choose to stay silent on Slack when appropriate

Changes in: `Agent`

---

**7.** `Feature` — **Azure AI Foundry Support**

The AI agent can now connect to Azure AI Foundry as a backend with support for multiple Azure scopes.
- Agents on Azure infrastructure can use Azure AI Foundry as the AI provider
- Multiple Azure scopes supported per agent configuration

Changes in: `Agent`

---

**8.** `Enhancement` — **Bulk Ticket Creation Redesign**

Creating multiple AI tickets at once is now faster and more configurable.
- New split-pane layout separates task selection from per-task configuration (persona, skills, permissions)
- "Apply to checked" batch mode lets you configure multiple tasks at once
- Tickets auto-trigger AI execution immediately upon creation

Changes in: `Frontend`

---

**9.** `Enhancement` — **Prompt Suggestion Auto-Submit**

Clicking a prompt suggestion now immediately submits the request when a scope is active.
- Suggestions auto-submit when a scope is already selected, removing an extra click
- If no scope is selected, the scope dropdown highlights with an inline error message

Changes in: `Frontend`

---

**10.** `Enhancement` — **Persona Skills Provisioning**

Skills defined on personas are now included when provisioning agent skills.
- Persona-level skills merged into the main skills list before provisioning
- Duplicates deduplicated to prevent double-provisioning

Changes in: `Agent`

---

**11.** `Enhancement` — **Optional Credentials in Scope**

Credentials are no longer required for all scope types — only where they are necessary.
- Cloud, Kubernetes, and Source Control provider types still require credentials
- Other provider types can be scoped without credentials, reducing configuration friction

Changes in: `Backend`

---

**12.** `Enhancement` — **Azure AKS Credential Types**

Azure AKS clusters can now be configured with Service Principal or Managed Identity authentication.
- Two new credential types added: Service Principal and Managed Identity

Changes in: `Frontend`

---

## March 31–April 7, 2026

---

**1.** `Enhancement` — **Keycloak SSO Login**

Enterprises using Keycloak can now log into the AI helpdesk with their existing credentials.
- Keycloak added as a supported identity provider alongside Microsoft SSO
- Extra Keycloak parameters (realm, client ID, etc.) configurable via Helm

Changes in: `Backend`

---

**2.** `Enhancement` — **Configurable Google Login**

Admins can now disable Google login entirely, giving tighter control over which authentication methods are available for your deployment.
- Google login can be turned off independently per deployment
- Useful for enterprises that require SSO-only access policies

Changes in: `Backend`

---

**3.** `Feature` — **Azure Deployment Support**

The AI helpdesk can now be deployed on Azure infrastructure, expanding support beyond AWS.
- Azure-specific credential and configuration handling added to the backend
- Service Principal and Managed Identity authentication supported for AKS

Changes in: `Backend`

---

**4.** `Feature` — **Agent Dashboard Integration**

Agent activity now feeds directly into dashboard metrics, giving a live view of what agents are doing across your workspaces.
- Dashboard and agent views are more tightly integrated
- Supports ticket and link views within dashboard panels

Changes in: `Backend` `Frontend`

---

**5.** `Enhancement` — **Pulumi CLI Support**

The agent now has Pulumi CLI bundled, enabling infrastructure-as-code workflows using Pulumi.
- Works alongside existing tools like `kubectl`, `aws`, and `gcloud`
- Allows agents to manage cloud infrastructure declaratively via Pulumi

Changes in: `Agent`

---

**6.** `Enhancement` — **Multi-Origin Ticket Support**

Tickets can now be created from and attributed to multiple sources — Slack, API, web UI — with origin tracked on each ticket.
- Enables better routing, filtering, and audit trails across channels
- Origin data available for reporting and analytics

Changes in: `Backend`

---

**7.** `Feature` — **AI-Assisted Markdown Editor**

A new standalone markdown editor with built-in AI editing support is now available within the platform.
- Useful for drafting and refining system prompts, project descriptions, and documentation
- AI can assist with editing and improving markdown content inline

Changes in: `Frontend`

---

**8.** `Enhancement` — **Project Task as Opening Chat Message**

When creating a ticket from a project, the task description is now automatically posted as the first message in the conversation.
- The agent immediately sees the full context without requiring the user to re-type it
- Reduces friction for project-driven ticket workflows

Changes in: `Frontend`

---

**9.** `Enhancement` — **Workspace Reports Enhanced**

Workspace reports now include project files and ticket names, giving a more complete view of all activity and output within a workspace.
- Project files included in report generation
- Ticket names surfaced for better report organization

Changes in: `Backend`

---

**10.** `Enhancement` — **Cost Optimization: Smarter Agent Planning**

The agent's planning and spec-writing prompts now only activate for ticket types that actually require them, reducing unnecessary token usage.
- Cuts cost on routine tasks without affecting quality on complex ones

Changes in: `Agent`

---

## March 24–31, 2026

---

**1.** `Feature` — **Stop Generation Mid-Response**

You can now stop the AI agent while it's actively generating a response or running a task.
- A stop button appears during streaming and immediately cancels the in-progress task
- Works across both chat streaming and background agent task execution
- No need to wait for a long task to complete before starting a new one

Changes in: `Agent` `Frontend`

---

**2.** `Feature` — **Scheduled Ticket Execution**

Tickets can now be scheduled to run automatically at a defined time — useful for recurring tasks, nightly checks, or timed automation without manual triggering.
- Schedule configured at ticket creation or update time
- Runs the ticket silently at the scheduled time

Changes in: `Backend`

---

**3.** `Feature` — **Microsoft SSO Login**

The AI helpdesk now supports Microsoft Single Sign-On for authentication, allowing users to log in with their existing Microsoft/Azure AD credentials.
- Integrates with existing Microsoft/Azure AD identity providers
- No separate password or account creation required

Changes in: `Backend`

---

**4.** `Enhancement` — **Multiple Personas per Workspace**

Workspaces now support multiple personas, giving more flexibility in how the AI behaves across different use cases within the same workspace.
- When creating a ticket, you can choose which persona to use for that conversation
- System prompt field removed from ticket creation — persona handles this instead

Changes in: `Frontend`

---

**5.** `Feature` — **Skills on Tickets**

Skills can now be assigned to tickets at creation time and managed throughout the ticket lifecycle.
- Gives precise control over which capabilities the agent can use in each conversation
- Skills are protected from accidental removal in the selection UI

Changes in: `Frontend`

---

**6.** `Feature` — **GRC (Governance, Risk & Compliance) Provider Tab**

A new GRC provider category tab is now available in the admin providers panel, joining the existing IT and GTM categories.
- Allows GRC tool integrations to be organized separately from IT/GTM providers

Changes in: `Frontend`

---

**7.** `Feature` — **Auto Ticket Title Generation**

Tickets now automatically generate a descriptive title based on the conversation content, so you no longer need to manually name every ticket.
- Title is generated by the agent after the first exchange
- Displayed in the ticket list and header immediately after generation

Changes in: `Agent` `Backend`

---

**8.** `Feature` — **AKS (Azure Kubernetes Service) Provider Support**

The agent now supports Azure Kubernetes Service as a provider type, expanding the range of cloud infrastructure it can work with.
- AKS clusters can be connected and managed via the agent
- Works alongside existing AWS and GCP provider support

Changes in: `Agent`

---

**9.** `Feature` — **GCP System Credential Support**

GCP system-level credentials are now supported, enabling deeper integration with Google Cloud infrastructure without per-user credential setup.
- System credentials apply across the workspace rather than per user
- Simplifies GCP-heavy deployments

Changes in: `Backend`

---

**10.** `Feature` — **Reports & Analytics API**

New reporting APIs are now available, laying the groundwork for analytics and reporting features within the AI helpdesk.
- Provides the data foundation for future reporting dashboards
- API-first design allows external tools to query report data

Changes in: `Backend`

---

**11.** `Enhancement` — **HTML Artifact Viewer Improvements**

HTML artifacts can now be viewed in fullscreen mode, and external links show a confirmation before navigating away.
- Dedicated expand button opens artifacts in a fullscreen overlay
- Prevents accidental navigation away from the current session

Changes in: `Frontend`

---

## March 17–24, 2026

---

**1.** `Feature` — **Real-Time Streaming Chat**

AI responses now stream to your screen as they are generated, rather than waiting for the full response to complete.
- Fixed intermittent cases where streaming would stall or produce malformed output
- Collaborative messages from other users in the same session now also appear in real-time

Changes in: `Backend` `Frontend`

---

**2.** `Feature` — **System Prompts for Workspaces, Projects & Personas**

You can now define custom system prompts on workspaces, projects, and personas to shape how the AI behaves in that context.
- System prompts render with full markdown formatting
- Viewable inline on the detail page; longer prompts open in a modal for easier reading
- Prompts defined at each level are automatically passed to the agent during conversations

Changes in: `Backend` `Frontend`

---

**3.** `Feature` — **Long-Lived API Tokens**

Users can now generate personal API tokens to authenticate with the AI helpdesk programmatically — useful for integrations and automation without interactive login.
- Tokens have configurable expiry dates; the last 4 characters are shown as a hint for easy identification
- Tokens can be revoked (active) or permanently deleted (expired/revoked) by the user
- Admins can view and manage all tokens across users from the Access Control panel

Changes in: `Backend` `Frontend`

---

**4.** `Enhancement` — **Ticket Name Prefixes**

Workspaces now support a short name field used as a prefix when generating ticket names, making tickets easier to identify across workspaces.
- Short names must be unique within a workspace and start with a letter
- Editable on both create and edit workspace forms

Changes in: `Backend` `Frontend`

---

**5.** `Feature` — **Ticket Summaries**

Tickets now automatically generate a compacted summary of the conversation, giving you a quick overview without scrolling through the full history.

Changes in: `Backend`

---

**6.** `Feature` — **Edit Ticket Scopes from Chat**

You can now reassign which integrations/tools (scopes) a ticket has access to directly from the chat interface — no need to recreate the ticket.
- At least one scope must remain selected
- Changes take effect immediately with success feedback

Changes in: `Backend` `Frontend`

---

**7.** `Enhancement` — **User Identity in Chat Messages**

Chat messages now show who sent them — display name (with fallback to email) and a color avatar.
- Makes it easier to follow conversations with multiple participants
- Mentions in activity chat now show user avatars and display names in the dropdown

Changes in: `Backend` `Frontend`

---

**8.** `Enhancement` — **Unread Message Badge**

The activity sidebar now displays an unread message count badge so you can see new messages arriving without keeping the chat panel open.
- Badge updates in real-time as new messages arrive
- Clears when the chat panel is opened

Changes in: `Frontend`

---

**9.** `Feature` — **Observability & Security Dashboards**

New dashboard views for Observability and Security metrics are now available in the admin panel.

Changes in: `Backend` `Frontend`

---

**10.** `Enhancement` — **Command Output in Chat**

Long command outputs in chat are now collapsed by default for a cleaner view, with a clear expand control to see the full output when needed.
- Expandable/collapsible with hover tooltips

Changes in: `Frontend`

---

## DuploCloud AI Suite Release — September 5, 2025

### Overview

We're excited to introduce **DuploCloud AI Suite**, a comprehensive artificial intelligence platform that transforms how you manage cloud infrastructure. This inaugural release brings intelligent automation to DevOps workflows through specialized AI Agents that work alongside your team to solve complex infrastructure challenges.

### What's New

#### AI Studio

**Build and Deploy Custom AI Agents**

AI Studio provides everything you need to create, customize, and deploy AI Agents tailored to your organization's needs:

* **Agent Specification Builder** - Define your Agent's capabilities and behavior
* **Vector Database Support** - Enable Agents to access and search your documentation and knowledge base
* **One-Click Deployment** - Automatically deploy Agents to Kubernetes
* **Agent Registration** - Seamlessly register deployed Agents into HelpDesk for immediate use

#### HelpDesk

**Intelligent Support with Human Oversight**

HelpDesk transforms traditional IT support through AI-powered assistance while maintaining complete human control:

**Smart Ticketing System**

* Create tickets and get matched with the most appropriate AI Agent
* View, search, and filter tickets
* Track Agent assignments and ticket status in real time

**Collaborative AI Assistance**

* **Human-in-the-Loop Approval** - All Agent actions require your explicit approval before execution
* **Shared Canvas** - Work side-by-side with AI Agents in a collaborative workspace
* **Interactive Terminal** - Share a live terminal where both you and the Agent can run commands
* **File Collaboration** - Agents can generate configuration files that you can edit and refine
* **Rich Content Support** - Full Markdown rendering with interactive Mermaid diagrams

**Advanced Security Controls**

* **Double Approval** - Sensitive commands require additional confirmation for extra security
* **Credential Proxying** - Agents use your permissions, never their own
* **Smart Prompt Suggestions** - Get started quickly with Agent-specific conversation starters

**Flexible Access**

* **Standalone Interface** - Full-featured HelpDesk application
* **Chat Bubble Integration** - Quick access from anywhere in the DuploCloud platform

### Available AI Agents

#### Kubernetes Agent

Your intelligent Kubernetes troubleshooting companion that can:

* Diagnose deployment issues and container problems
* Create new deployments and services
* Perform cluster maintenance and optimization tasks
* Provide expert guidance on Kubernetes best practices

#### Observability Agent

Powered by DuploCloud's Advanced Observability Suite, this Agent helps you:

* Retrieve and analyze metrics and logs for any microservice
* Identify performance bottlenecks and anomalies
* Get intelligent insights from your OpenTelemetry data
* **Coming soon:** Trace analysis and performance profiling

#### CI/CD Agent

Intelligent pipeline support that automatically:

* Monitors your Jenkins and GitHub Actions pipelines
* Creates support tickets when builds fail
* Attaches relevant logs, configuration, and error details
* Provides expert troubleshooting assistance for pipeline issues

#### Architecture Diagram Agent

Transform complex infrastructure into clear visuals:

* Generate architecture diagrams using natural language descriptions
* Automatically map relationships between services, databases, and infrastructure
* Create shareable Mermaid diagrams of your entire technology stack

#### Private GPT Agent

Secure AI assistance for security-conscious organizations:

* Private ChatGPT-like experience using AWS Bedrock
* Complete data privacy with enterprise-grade security
* Perfect for teams who need AI assistance without third-party data sharing

### Supporting Infrastructure

#### DuploCloud Cartography

* **Automatic Discovery** - Continuously maps your AWS, Kubernetes, and DuploCloud resources
* **Relationship Mapping** - Understands dependencies between microservices and infrastructure
* **Custom Dependencies** - Define application-specific relationships for complete visibility

#### DuploCloud Presidio

* **Data Protection** - Automatically redacts sensitive information in AI conversations
* **Customizable Rules** - Configures what data should be protected based on your security policies
* **Privacy-First** - Ensures sensitive data never leaves your environment

### Key Benefits

**Intelligent Automation** - AI Agents that understand your infrastructure and can take action with your approval

**Security First** - Human oversight for all actions with your credentials, never autonomous access

**Faster Resolution** - Collaborative workspace where you and AI work together to solve problems

**Better Insights** - Automatic diagram generation and intelligent analysis of your systems

**Enterprise Ready** - Private AI models with complete data privacy and security controls
