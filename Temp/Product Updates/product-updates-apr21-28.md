# Product Updates — April 21–28, 2026

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
