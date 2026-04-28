# Product Updates

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

**5.** `Feature` — **Core MCP Component in Helm + IRSA Support**
The Helm chart now includes an optional DuploCloud platform MCP server component, and both agent and backend pods support IRSA role annotations.
- New `coreMcp` component can be enabled independently with its own ingress path
- IRSA role ARN can be set per component in values — the annotation is injected automatically
- Fully backwards compatible — existing deployments are unaffected unless new values are set

Changes in: `Helm`

---

**6.** `Feature` — **Bedrock Model Auto-Subscription**
A Helm-managed job now automatically accepts AWS Bedrock model access agreements during install or upgrade.
- Runs as a post-install hook using a dedicated IAM role — no manual AWS console steps needed
- The list of models to subscribe to is configurable in Helm values
- Failures surface with clear diagnostic output rather than silent errors

Changes in: `Helm`

---

**7.** `Feature` — **Agent Sandbox Enhancements**
Agents can now access workspace and project directories automatically, and run Python-based MCP servers out of the box.
- Workspace and project folders are mounted into the agent sandbox based on the platform context — no manual path configuration needed
- Python MCP servers using the `uvx` pattern (e.g. `uvx mcp-grafana`) are now supported
- The sandbox can be disabled via environment variable for deployments that require it

Changes in: `Agent`

---

**8.** `Enhancement` — **Backend Context & Session Reliability**
Several improvements make agent sessions more reliable and context-aware across EKS and multi-scope environments.
- Workspace and project identifiers are now included in the agent's operating context
- Tickets with partially invalid scope configurations now process successfully using the valid scopes
- EKS authentication tokens have an extended validity window for longer-running sessions

Changes in: `Backend`

---

**9.** `Enhancement` — **Service Desk UX & Entity Awareness**
The Service Desk UI is clearer when workspace configuration has changed, and easier to navigate.
- Scopes, personas, and skills that have been removed now show a "Removed" badge with a tooltip instead of a raw ID
- Scope type (EKS, GitHub, etc.) is shown in the scope selection dropdown
- The "View Ticket Details" action is now available in all ticket view modes, and the agent selector is shown consistently during bulk ticket creation

Changes in: `Frontend`

---

**10.** `Enhancement` — **Streaming Error Resilience**
Agent streaming is more robust against errors, and usage cost reporting no longer double-counts.
- Errors during streaming now surface as notifications in the UI rather than silently dropping the response
- Session cost is reported once at the end of the session rather than incrementally, preventing over-reporting
- Slack-routed messages are handled distinctly from multi-message threads for more consistent behavior

Changes in: `Backend` `Agent`

---

**11.** `Enhancement` — **Agent Max Turns Increased to 100**
The default maximum number of agent turns per session has been raised to support longer-running tasks out of the box.
- Default raised to 100 turns per session
- Can be overridden per deployment via environment variable
- Per-session cost budget cap remains configurable independently

Changes in: `Agent`

---

## April 7–14, 2026

---

**1.** `Feature` — **Cross-Workspace Report Sharing**
Share AI reports with other workspaces directly from the report menu.
- Reports can be shared with one or more workspaces via a multi-select dialog; shared reports appear in recipient workspaces with a clear indicator
- Recipients can remove themselves without contacting the report owner
- Backend enforces owner-only patching, tracks sharedBy/sharedAt metadata, and adds a MongoDB index for query performance

Changes in: `Backend` `Frontend`

---

**2.** `Feature` — **Workspace & Project Secrets Management**
Sensitive credentials can now be stored securely at the workspace, project, and ticket level.
- Secrets are encrypted at rest using MongoDB Client-Side Field Level Encryption (CSFLE) with AES-256
- Encryption master key is auto-generated in Helm; supports future migration to AWS KMS
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
- Credential data migrated to an encrypted DataEx format with per-field type and sensitivity markers
- Supports arbitrary custom key-value fields with types: string, secret, certificate, and more
- UI provides a scrollable modal for managing structured credentials with inline editing

Changes in: `Backend` `Frontend`

---

**5.** `Feature` — **Private Git Repository Skills**
AI skills can now be loaded directly from private Git repositories.
- Backend validates repository credentials and clones the repo into the skill directory on creation/update
- Skills support a new PrivateGitRepo format type with configurable org, repo, branch, and folder path
- Admin UI includes a Git repository configuration form within the Add/Edit skill workflow

Changes in: `Backend` `Frontend`

---

**6.** `Feature` — **Slack Integration**
The AI agent can now receive and respond to messages from Slack.
- Messages from Slack are tagged with a `[slack]` prefix and processed with Slack-specific instructions
- The agent can choose to stay silent on Slack by responding "Roger." — suppressing output cleanly
- DoneEvent reports a `stop_reason` of `slack_silence` for silent responses

Changes in: `Agent`

---

**7.** `Feature` — **Azure AI Foundry Support**
The AI agent can now connect to Azure AI Foundry as a backend with support for multiple Azure scopes.
- Agents on Azure infrastructure can use Azure AI Foundry as the AI provider
- Multiple Azure scopes supported per agent configuration
- Controlled via the `CLAUDE_CODE_USE_FOUNDRY` environment variable

Changes in: `Agent`

---

**8.** `Enhancement` — **Platform Skills Refactoring**
Platform-level skills are now seeded from the database instead of being hardcoded per project.
- Project-specific logic removed from the agent; skills stored and managed centrally in the DB
- Skills routed via `OriginContext.subType` for cleaner handling of dashboard and project tickets
- UI skill-mapping form updated to reflect the new backend structure

Changes in: `Backend` `Frontend` `Agent`

---

**9.** `Enhancement` — **Real-Time Chat Connection Reliability**
Significant improvements to SignalR connection stability and message streaming quality.
- Connection lifecycle refactored: reconnect handlers automatically re-subscribe users to active threads
- Streaming tokens buffered to avoid partial words mid-stream; emoji/Unicode handled correctly
- Double-stringified JSON in streamed messages resolved; duplicate approval via emoji comparison fixed

Changes in: `Frontend` `Agent`

---

**10.** `Enhancement` — **Bulk Ticket Creation Redesign**
Creating multiple AI tickets at once is now faster and more configurable.
- New split-pane layout separates task selection from per-task configuration (persona, skills, permissions)
- "Apply to checked" batch mode lets you configure multiple tasks at once
- Tickets auto-trigger AI execution immediately upon creation

Changes in: `Frontend`

---

**11.** `Enhancement` — **Prompt Suggestion Auto-Submit**
Clicking a prompt suggestion now immediately submits the request when a scope is active.
- Suggestions auto-submit when a scope is already selected, removing an extra click
- If no scope is selected, the scope dropdown highlights with an inline error message
- Error clears as soon as a scope is chosen

Changes in: `Frontend`

---

**12.** `Enhancement` — **Persona Skills Provisioning**
Skills defined on personas are now included when provisioning agent skills.
- Persona-level skills merged into the main skills list before provisioning
- Duplicates deduplicated by skill `Id` to prevent double-provisioning

Changes in: `Agent`

---

**13.** `Enhancement` — **Planning Skill as Provisioned File**
The planning system prompt is now a versioned skill file rather than embedded code.
- Planning and spec tickets load a `SKILL.md` from `.claude/skills/spec-plan-tasks` at runtime
- Single-document workflow enforced: agent asks approval before moving between spec, plan, and execution
- Tasks JSON schema strictly validated with required fields and no extra properties

Changes in: `Agent`

---

**14.** `Enhancement` — **Optional Credentials in Scope**
Credentials are no longer required for all scope types — only where they are necessary.
- Cloud, Kubernetes, and Source Control provider types still require credentials
- Other provider types can be scoped without credentials, reducing configuration friction
- Validation logic updated to be type-aware

Changes in: `Backend`

---

**15.** `Enhancement` — **Azure AKS Credential Types**
Azure AKS clusters can now be configured with Service Principal or Managed Identity authentication.
- Two new credential types added: Service Principal and Managed Identity
- Field cleanup logic removes irrelevant fields when switching between credential types

Changes in: `Frontend`

---

**16.** `Bug` — **Encryption Master Key Length Fix**
Fixed an issue where the auto-generated Helm encryption key was too short, causing decryption failures.
- Key is now generated using `randBytes 96 | b64enc`, decoding to exactly 96 bytes as required
- Previous alphanumeric generation only decoded to 72 bytes, causing silent encryption failures

Changes in: `Helm`

---

**17.** `Bug` — **xterm Kubeconfig Security Fix**
Kubernetes configuration is no longer exposed in socket URL query parameters.
- Kubeconfig now transmitted via dedicated socket events on connect and on-demand
- Prevents kubeconfig exposure in browser network logs and server access logs

Changes in: `Frontend`

---

**18.** `Bug` — **Provider Data Migration on Empty Dataset**
Migration no longer fails when there are no provider entries to process.
- Returns success immediately if the provider collection is empty
- Prevents spurious migration errors during fresh deployments

Changes in: `Backend`

---

## March 31–April 7, 2026

---

**1.** `Feature` — **AI Studio Merged into Main Platform**
The AI Studio is now built into the main DuploCloud platform — no separate app needed.
- Tickets, agents, workspaces, and personas are accessible directly from the main UI
- Users on the platform can access AI features without switching apps
- Merged via a single large integration PR covering all AI Studio components

Changes in: `Frontend`

---

**2.** `Feature` — **Keycloak SSO Login**
Enterprises using Keycloak can now log into the AI helpdesk with their existing credentials.
- Keycloak added as a supported identity provider alongside Microsoft SSO
- Extra Keycloak parameters (realm, client ID, etc.) configurable via Helm
- Joins Microsoft SSO added the previous week

Changes in: `Backend`

---

**3.** `Feature` — **Configurable Google Login**
Admins can now disable Google login entirely, giving tighter control over which authentication methods are available for your deployment.
- Google login can be turned off independently per deployment
- Useful for enterprises that require SSO-only access policies

Changes in: `Backend`

---

**4.** `Feature` — **Azure Deployment Support**
The AI helpdesk can now be deployed on Azure infrastructure, expanding support beyond AWS.
- Azure-specific credential and configuration handling added to the backend
- Service Principal and Managed Identity authentication supported for AKS

Changes in: `Backend`

---

**5.** `Feature` — **Tickets Remember Their Persona**
Tickets now store which persona was selected at creation, preserving AI behavior context for the full lifecycle of the conversation.
- Persona is saved on the ticket and passed to the agent on every message
- Enables persona-based filtering and reporting across workspaces

Changes in: `Backend` `Frontend`

---

**6.** `Feature` — **Agent Dashboard Integration**
Agent activity now feeds directly into dashboard metrics, giving a live view of what agents are doing across your workspaces.
- Dashboard and agent views are more tightly integrated
- Supports ticket and link views within dashboard panels

Changes in: `Backend` `Frontend`

---

**7.** `Feature` — **Script Execution via Agent**
The agent can now execute scripts directly as part of task processing, unlocking more complex automation workflows.
- Supports running custom scripts beyond standard CLI commands
- Scripts are executed in the agent's sandboxed environment

Changes in: `Agent`

---

**8.** `Feature` — **Pulumi CLI Support**
The agent now has Pulumi CLI bundled, enabling infrastructure-as-code workflows using Pulumi.
- Works alongside existing tools like `kubectl`, `aws`, and `gcloud`
- Allows agents to manage cloud infrastructure declaratively via Pulumi

Changes in: `Agent`

---

**9.** `Feature` — **Sales Prospecting Skills**
New sales prospecting capabilities are now available to the agent, supporting GTM workflows.
- Ties into the Apollo, Outreach, and other GTM providers added in recent weeks
- Agent can perform outreach research and prospecting as a built-in skill

Changes in: `Agent`

---

**10.** `Feature` — **API Audit Skill**
The agent can now perform API audits as a built-in skill — useful for reviewing API usage and identifying undocumented endpoints.
- Helps ensure API hygiene across services
- Available as a skill that can be assigned to tickets and agents

Changes in: `Agent` `Backend`

---

**11.** `Feature` — **Multi-Origin Ticket Support**
Tickets can now be created from and attributed to multiple sources — Slack, API, web UI — with origin tracked on each ticket.
- Enables better routing, filtering, and audit trails across channels
- Origin data available for reporting and analytics

Changes in: `Backend`

---

**12.** `Feature` — **AI-Assisted Markdown Editor**
A new standalone markdown editor with built-in AI editing support is now available within the platform.
- Useful for drafting and refining system prompts, project descriptions, and documentation
- AI can assist with editing and improving markdown content inline

Changes in: `Frontend`

---

**13.** `Enhancement` — **Project Task as Opening Chat Message**
When creating a ticket from a project, the task description is now automatically posted as the first message in the conversation.
- The agent immediately sees the full context without requiring the user to re-type it
- Reduces friction for project-driven ticket workflows

Changes in: `Frontend`

---

**14.** `Enhancement` — **Workspace Reports Enhanced**
Workspace reports now include project files and ticket names, giving a more complete view of all activity and output within a workspace.
- Project files included in report generation
- Ticket names surfaced for better report organization

Changes in: `Backend`

---

**15.** `Enhancement` — **Cost Optimization: Smarter Agent Planning**
The agent's planning and spec-writing prompts now only activate for ticket types that actually require them, reducing unnecessary token usage.
- Cuts cost on routine tasks without affecting quality on complex ones
- Planning prompts scoped to `plan_creation` and `spec_creation` ticket types only

Changes in: `Agent`

---

**16.** `Enhancement` — **Helm / Infrastructure**
Terminal (xterm) enabled by default, persistent sessions, and zero-downtime rolling updates added to the Helm chart.
- xterm enabled by default — no manual config needed to get terminal access
- Flask secret key added so terminal sessions survive pod restarts
- Zero-downtime rolling updates configured for xterm and Slack backend deployments

Changes in: `Helm`

---

**17.** `Bug` — **Credential Cleanup After Each Session**
Cloud credentials are now automatically wiped from temporary storage after every agent session.
- Closes a potential window where credentials could linger on disk between task runs
- Applies to all cloud credential types (AWS, GCP, Azure)

Changes in: `Agent`

---

**18.** `Bug` — **Security Improvements**
Several security issues identified in an internal review have been addressed.
- Fixes to permission set group caching and data access controls
- Prevents unauthorized access to cross-workspace data

Changes in: `Backend`

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

**4.** `Feature` — **Multiple Personas per Workspace**
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
- Consistent with the multi-category provider navigation pattern

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

**11.** `Feature` — **v1.0.0 Release**
The AI Helpdesk backend has been bumped to v1.0.0, marking the first major stable release.
- Signals production readiness of the core platform
- Versioning now follows semantic versioning

Changes in: `Backend`

---

**12.** `Enhancement` — **HTML Artifact Viewer Improvements**
HTML artifacts can now be viewed in fullscreen mode, and external links show a confirmation before navigating away.
- Dedicated expand button opens artifacts in a fullscreen overlay
- Prevents accidental navigation away from the current session

Changes in: `Frontend`

---

**13.** `Enhancement` — **API Token Enhancements**
Building on last week's long-lived token feature — tokens can now be searched and linked to group users.
- Tokens searchable by name or value for easier management
- Tokens can be linked to group users for shared access scenarios

Changes in: `Backend` `Frontend`

---

**14.** `Enhancement` — **Clearer Validation Error Messages**
When a request references entities that don't exist, you now get clear error messages listing exactly which entities are missing.
- Replaces generic failure messages with actionable details
- Applies across workspace, project, and ticket validation

Changes in: `Backend`

---

**15.** `Enhancement` — **Real-Time Ticket Processing Status**
The ticket status is now updated immediately when processing begins, so the UI reflects that the agent is working as soon as a message is sent.
- No longer waits for the first agent response to show "processing" status
- Improves perceived responsiveness for users waiting on long tasks

Changes in: `Backend`

---

**16.** `Enhancement` — **Streaming Reliability Improvements**
Under-the-hood improvements to how streaming messages are buffered and synchronized, reducing out-of-order or missing chunks.
- Buffering logic improved for long agent responses
- Reduces visible glitches in streamed output

Changes in: `Agent` `Frontend`

---

**17.** `Enhancement` — **Generic Scope Type Support**
The agent can now handle custom or non-standard scope/provider types generically, rather than failing on unrecognized types.
- New integrations can be used even before explicit agent support is added
- Reduces the need for code changes when onboarding new provider types

Changes in: `Agent`

---

**18.** `Enhancement` — **Helm / Infrastructure**
Auto-scaling, graceful shutdown, and routing improvements added to the Helm chart.
- HPA (Horizontal Pod Autoscaler) and graceful shutdown added for the duploAgent
- DuploMasterUrl added to ingress routing for better compatibility with DuploCloud portal deployments
- Fixed backend startup issue caused by missing `INFRA_REGION` environment variable

Changes in: `Helm`

---

## March 17–24, 2026

---

**1.** `Feature` — **Real-Time Streaming Chat**
AI responses now stream to your screen as they are generated, rather than waiting for the full response to complete.
- Fixed intermittent cases where streaming would stall or produce malformed output
- Collaborative messages from other users in the same session now also appear in real-time
- Fixed connection timing issues that could cause messages to be missed on load

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

**4.** `Feature` — **Ticket Name Prefixes**
Workspaces now support a short name field used as a prefix when generating ticket names, making tickets easier to identify across workspaces.
- Short names must be unique within a workspace and start with a letter
- Editable on both create and edit workspace forms

Changes in: `Backend` `Frontend`

---

**5.** `Feature` — **Ticket Summaries**
Tickets now automatically generate a compacted summary of the conversation, giving you a quick overview without scrolling through the full history.
- Summary logic runs as a service layer operation, not a hook
- Accessible via a dedicated API endpoint

Changes in: `Backend`

---

**6.** `Feature` — **Edit Ticket Scopes from Chat**
You can now reassign which integrations/tools (scopes) a ticket has access to directly from the chat interface — no need to recreate the ticket.
- At least one scope must remain selected
- Changes take effect immediately with success feedback

Changes in: `Backend` `Frontend`

---

**7.** `Feature` — **Sales & Marketing (GTM) Provider Support**
A new Sales & Marketing provider category is now available alongside the existing IT providers.
- Sales: Apollo, Outreach, Zoom, Attention, Gong; Marketing: HubSpot
- Organized in a dedicated GTM tab in the admin providers panel, separate from IT providers
- Provider navigation menu restructured into collapsible IT and GTM sub-sections

Changes in: `Backend` `Frontend`

---

**8.** `Feature` — **User Identity in Chat Messages**
Chat messages now show who sent them — display name (with fallback to email) and a color avatar.
- Makes it easier to follow conversations with multiple participants
- Mentions in activity chat now show user avatars and display names in the dropdown
- Current user is automatically excluded from the mention list

Changes in: `Backend` `Frontend`

---

**9.** `Feature` — **Unread Message Badge**
The activity sidebar now displays an unread message count badge so you can see new messages arriving without keeping the chat panel open.
- Badge updates in real-time as new messages arrive
- Clears when the chat panel is opened

Changes in: `Frontend`

---

**10.** `Feature` — **Observability & Security Dashboards**
New dashboard views for Observability and Security metrics are now available in the admin panel, backed by a new metrics and policy data model.
- Separated and refactored metric model classes for extensibility
- Model objects for Dashboard entities added to the backend

Changes in: `Backend` `Frontend`

---

**11.** `Enhancement` — **Command Output in Chat**
Long command outputs in chat are now collapsed by default for a cleaner view, with a clear expand control to see the full output when needed.
- Expandable/collapsible with hover tooltips
- Auto-scroll behavior improved so the terminal doesn't hijack your scroll position

Changes in: `Frontend`

---

**12.** `Enhancement` — **Command Execution Permissions Redesign**
The UI for configuring which commands an agent can run automatically has been redesigned with clearer toggle cards, replacing the previous layout.
- Labels are now "auto-approval" and "auto-rejection" for better clarity
- Replaces the previous ambiguous layout

Changes in: `Frontend`

---

**13.** `Enhancement` — **Ticket List Improvements**
The ticket list now shows a Created By column and a Copy Ticket Name quick action.
- Created By column shows who opened each ticket at a glance
- Copy Ticket Name available from the ticket actions dropdown
- Long ticket titles now show a tooltip on hover instead of truncating silently

Changes in: `Frontend`

---

**14.** `Enhancement` — **Helm / Infrastructure**
Helm chart updated with MongoDB backups, configurable Claude model version, and DuploCloud MCP server bundled by default.
- MongoDB backups now configured in Helm for data durability
- Claude model version is now configurable via an environment variable
- DuploCloud MCP server enabled by default; shared output volume added for cross-ticket processing

Changes in: `Helm`

---

**15.** `Bug` — **Secure Credential Injection in Terminal**
AWS, GCP, and Kubernetes credentials are now injected securely into terminal sessions behind the scenes — no longer visible as `export` commands in terminal output.
- Credentials sent via Socket.IO events instead of shell export commands
- Reduces credential exposure risk in terminal output and URL parameters

Changes in: `Frontend`

---

**16.** `Bug` — **Agent Session Stability**
Fixed an issue where long-running agent sessions would silently drop their connection mid-task.
- Sessions can now stay active for up to 30 minutes without timing out
- Improved agent instructions for more consistent file handling behavior

Changes in: `Agent`

---

**17.** `Bug` — **Security Fix: Blocked Path Traversal**
Fixed a security vulnerability where specially crafted document requests could access files outside the intended directory scope.
- Path traversal attempts are now blocked at the agent level
- No user action required

Changes in: `Agent`

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

**🤖 Intelligent Automation** - AI Agents that understand your infrastructure and can take action with your approval

**🛡️ Security First** - Human oversight for all actions with your credentials, never autonomous access

**🚀 Faster Resolution** - Collaborative workspace where you and AI work together to solve problems

**📊 Better Insights** - Automatic diagram generation and intelligent analysis of your systems

**🔒 Enterprise Ready** - Private AI models with complete data privacy and security controls
