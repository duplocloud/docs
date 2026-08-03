# AI Guardrails

DuploCloud enforces multiple layers of guardrails on every agent interaction. These controls are designed to make bad outcomes structurally impossible rather than relying solely on model-level instruction-following.

Guardrails fall into two categories: **platform-level controls** that are always active, and **LLM provider guardrails** that are optionally enabled at the cloud provider level.

---

## Platform Guardrails

The following controls are enforced by the DuploCloud platform on every ticket, regardless of which LLM is in use.

### Scoped, Just-in-Time Credentials

The agent receives temporary credentials generated from the Scope assigned to the ticket. Those credentials carry only the permissions you defined for that Scope. If the Scope does not include permission to access a particular resource or environment, the agent cannot reach it — not because it has been instructed not to, but because the credentials do not allow it.

Credentials are never passed to the agent directly or stored in session context. They are generated at execution time and expire when the ticket closes.

### Read-Only by Default

The agent operates in read-only mode unless write permissions have been explicitly granted. Remediation actions — anything that modifies infrastructure — require human approval before execution.

### Human Approval Workflow

Every proposed command or infrastructure change is surfaced to an engineer for review before it is applied. The agent proposes; the engineer approves. No action is taken autonomously on infrastructure.

For a full description of the approval flow, see [Human Approval Requirements](../tickets.md).

### MCP Tool Call Approval

External [MCP server](../mcp-servers/README.md) tool calls go through the same kind of gate — every call an agent wants to make to an MCP tool is surfaced in chat for approval first. Previously, MCP tools executed automatically the moment a scope granted access to them; there was no approval step at all.

The card in chat shows **"I can run the following tools for you:"**, listing each tool with its name and an **MCP: `<server-name>`** badge. Expand **Details** to see the MCP server, description, and the exact inputs the agent wants to pass. Three actions are available: **Approve**, **Reject** (opens a reason field), or **Ignore**.

{% hint style="info" %}
There's no "always allow" option — every MCP tool call is gated individually, regardless of how many times that tool has been approved before. This is separate from the [Command Execution Permissions](../tickets.md) auto-approve/auto-reject patterns, which apply only to shell commands, not MCP tools.
{% endhint %}

If you don't act on a pending approval right away, it doesn't time out or error — it stays exactly as-is, actionable indefinitely, even across page reloads or if you come back days later. Approving it later picks the tool call back up without needing to repeat any context.

### RBAC

Access is controlled at the Workspace and Scope level. Users are granted access only to the environments and resources assigned to them through [Permission Sets](permission-sets.md) and [User Groups](user-groups.md). A user with read-only access to a production Scope cannot escalate to write access within that session.

### Skills-Based Guardrails

Operational standards, security policies, and environment restrictions are encoded as [Skills](../skills/README.md) and included in the agent's system prompt. Skills are explicit, versioned instructions evaluated before execution — they are not model-dependent inference that could vary between runs. This is how domain constraints are applied consistently to every task.

### Audit Logging

Every ticket maintains a complete record of:
- What the agent was asked to do
- Every command or change the agent proposed
- The approval that preceded each execution step
- The outcome of every action taken

All agent actions are also executed through standard cloud and infrastructure interfaces (AWS API, kubectl, etc.), so they appear in your existing cloud provider audit logs independently of DuploCloud. If an incident needs investigation, you can trace through both layers: the DuploCloud ticket for intent and approval, and your cloud provider's logs for the corresponding API calls with credentials and timestamps.

### Environment Restrictions

Agents are scoped to specific environments. An agent scoped to Kubernetes operations has no access to Git credentials or AWS — it can only act within its defined Scope. Scopes can be further segmented by environment (e.g. staging vs. production), so a developer with full access to non-production has no write access to production infrastructure.

### Secret Redaction

The HelpDesk backend scrubs all registered secret values from both inputs before they reach the agent and from outputs before they reach the user. Credentials and sensitive values are replaced with `[REDACTED]` at the application layer before anything is forwarded to the LLM.

### Session Isolation

Each agent session is confined to its own isolated filesystem directory. There is no cross-session or cross-customer data access — context from one ticket cannot leak into another.

---

## LLM Provider Guardrails

In addition to platform-level controls, customers can enable server-side guardrails at the LLM API level. These are enforced by the cloud provider before any response is returned to the agent, providing an additional layer of content filtering and PII redaction independent of DuploCloud.

The following providers are supported:

| Provider | Product |
|---|---|
| AWS | Bedrock Guardrails |
| Azure | Azure AI Content Safety (Azure AI Foundry) |
| GCP | Vertex AI Safety Filters |

### AWS Bedrock Guardrails

Bedrock Guardrails are deployed via CloudFormation into the **customer's own AWS account**. Evaluation happens entirely within the customer's AWS boundary — no content is sent to an external evaluation service.

Three policy types are active:

**Content filters** — applied to both model inputs and outputs:

| Category | Level |
|---|---|
| Hate | HIGH / BLOCK |
| Insults | HIGH / BLOCK |
| Sexual | HIGH / BLOCK |
| Violence | HIGH / BLOCK |
| Misconduct | HIGH / BLOCK |
| Prompt Attack / Jailbreak | HIGH / BLOCK (input only) |

**PII anonymization** — the following types are masked in all model responses before they reach the user:

`EMAIL`, `PHONE`, `IP_ADDRESS`, `PASSWORD`, `AWS_ACCESS_KEY`, `AWS_SECRET_KEY`, `USERNAME`, `NAME`, `SSN`

**Denied topics** — requests in the following categories are blocked outright:
- Exfiltrating credentials or secrets
- Deleting infrastructure
- Creating backdoors
- Disabling audit controls or logging

#### Enabling Bedrock Guardrails

**Globally** — set the following environment variables in the Helm chart. This applies the guardrail as HTTP headers on every Bedrock Converse API call automatically:

```
BEDROCK_GUARDRAIL_IDENTIFIER = <GuardrailId from CloudFormation output>
BEDROCK_GUARDRAIL_VERSION = 1
```

**Per workspace** — the Workspace model includes a `GuardrailId` field that allows different guardrail configurations per customer or environment in a multi-tenant deployment. This is useful when different workspaces have different compliance requirements.

---

## Summary

| Control | Always On | Optional |
|---|---|---|
| Scoped, just-in-time credentials | ✓ | |
| Read-only by default | ✓ | |
| Human approval before execution | ✓ | |
| MCP tool call approval | ✓ | |
| RBAC (Workspace and Scope level) | ✓ | |
| Skills-based operational guardrails | ✓ | |
| Audit logging (platform + cloud provider) | ✓ | |
| Environment isolation | ✓ | |
| Secret redaction (application layer) | ✓ | |
| Session isolation | ✓ | |
| LLM provider content filters (Bedrock, Azure, GCP) | | ✓ |
| PII anonymization (Bedrock) | | ✓ |
| Denied topic enforcement (Bedrock) | | ✓ |
