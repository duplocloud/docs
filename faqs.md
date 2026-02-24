---
description: >-
  If your question isn't answered here, reach out to the team at
  support@duplocloud.com or contact us on Slack.
---

# FAQs

## Security & Access

<details>

<summary>Do we need full admin access?</summary>

No. You don't need to grant any access to get started. DuploCloud's stack runs as a few Docker containers alongside a MongoDB instance and two S3 buckets — no privileged access to your environment is required upfront.

Access is granted on your terms through [Providers](introduction/ai-devops-policy-model/providers.md) and Scopes. The platform uses IAM permissions defined in each Scope to generate temporary, just-in-time credentials that are passed to the agent as part of the ticket. You control exactly what the agent can and cannot touch.&#x20;

</details>

<details>

<summary>How do you give access to Git?</summary>

Git is modeled as a Provider — the same way AWS, Kubernetes, and observability tools are. To give an Engineer Git access:

1. Navigate to **Providers** and add your Git provider (GitHub, GitLab, or Bitbucket).
2. Add your repository credentials under the **Credentials** tab.
3. Create a **Scope** — a named token with defined boundaries over specific repositories.
4. When creating a ticket, select the appropriate Scope.

See [Providers](introduction/ai-devops-policy-model/providers.md) for step-by-step instructions.

</details>

<details>

<summary>How are credentials stored and secured?</summary>

Credentials are stored in DuploCloud or referenced from your own secrets manager. The platform uses them to generate scoped, temporary access at execution time — credentials are never passed to agents directly or stored in session context.

Each Scope defines the exact resources an Engineer can access. Guardrails can further restrict specific resources, operations, or environments within that Scope. See [AI DevOps Policy Model](introduction/ai-devops-policy-model/) — Provider and Scope.

</details>

<details>

<summary>What is the audit trail for AI actions?</summary>

Every ticket maintains a full context and audit trail throughout its lifecycle — what the agent was asked to do, what it proposed, what was approved, and what was executed. The Engineer Hub surfaces this history per Engineer, providing a transparent record of all completed work. Completed task history is also stored in the Engineer's Knowledge Base, queryable for future reference.

</details>

<details>

<summary>What compliance certifications does DuploCloud have?</summary>

DuploCloud is SOC 2 certified. Full security documentation is available for procurement review. The platform is used by customers in regulated industries including fintech and healthcare. Contact [support@duplocloud.net](mailto:support@duplocloud.net) for compliance documentation.

</details>

## Pricing & Billing

<details>

<summary>What is the limit on the number of tokens?</summary>

There is no token-based billing. DuploCloud charges based on **tickets** (tasks completed) and **nodes under management** (infrastructure resources managed by the platform) — not on LLM token consumption. Think of it as the cost of a DevOps engineer for a fraction of the price. Contact the team for a business proposal with specific pricing assurances.

</details>

<details>

<summary>What exactly counts as a "ticket"?</summary>

A ticket is a unit of work assigned to an AI agent. In the workflow, a human approves a Task generated from a Project Plan — at that point, the Task becomes a Ticket and is dispatched to the appropriate agent for execution. Each ticket corresponds to one discrete, agent-executed action or investigation. See [AI Helpdesk - Tickets](ai-suite/ai-helpdesk/tickets.md) for details.

</details>

<details>

<summary>What does "nodes under management" mean?</summary>

Nodes under management refers to the infrastructure resources — servers, Kubernetes nodes, cloud instances — that DuploCloud actively monitors and operates on. This forms the second dimension of pricing alongside tickets, reflecting the scope of infrastructure the platform is responsible for.

</details>

<details>

<summary>What's included in the 30-day PoC?</summary>

The PoC gives you a working AI Engineer running against your real infrastructure. DuploCloud's human operations team — infrastructure engineers, Kubernetes specialists, and security practitioners — is included to support setup, review complex work, and ensure the PoC runs against tasks from your actual backlog. Contact the team to scope a PoC around your specific environment.

</details>

## Agents & Customisation

<details>

<summary>Do you use MCP servers or APIs to access AWS, Kubernetes, etc.?</summary>

It depends on the agent. For AWS and Kubernetes, the platform primarily uses the CLI — LLMs have strong CLI comprehension and it provides precise, auditable execution. For third-party systems that publish MCP servers (observability tools, ticketing systems, etc.), DuploCloud uses those MCP endpoints directly.

Agents are flexible. DuploCloud's core value is in the overall orchestration layer — individual agents can be modified or replaced for your specific environment. See [MCP Servers](introduction/ai-devops-policy-model/mcp-servers.md) for configuration details.

</details>

<details>

<summary>How do you handle long-running jobs?</summary>

The platform supports two communication modes:

* **Synchronous** — for short, fast-turnaround tasks where the result is returned inline.
* **Pub-sub (asynchronous)** — for long-running tasks such as code reviews that require a code checkout, analysis, and structured output. The agent publishes results when complete; no session needs to remain open.

Long-running tasks like generating code reviews or large deployments use the pub-sub model automatically.

</details>

<details>

<summary>Can we build custom agents or bring our own?</summary>

Yes. There are three options:

1. **Prebuilt Agents** — use DuploCloud's out-of-the-box agents as-is.
2. **Dynamic Agents** — build agents through the platform UI by defining a prompt, selecting tools, choosing an LLM, and deploying a container image.
3. **Bring your own** — connect an existing agent by providing its access endpoint. DuploCloud can also provide code for its own agents as a starting point.

See [Agents](ai-suite/ai-studio/agents.md) for setup instructions.

</details>

<details>

<summary>What agents come out of the box?</summary>

DuploCloud provides the following pre-built agents:

| Agent                      | What it does                                                                   |
| -------------------------- | ------------------------------------------------------------------------------ |
| SRE Agent                  | Orchestrates specialist sub-agents for broad incident and operations support   |
| Kubernetes Agent           | Cluster management, health checks, resource management, log analysis           |
| Observability Agent        | Monitoring and performance via OpenTelemetry and Grafana                       |
| CI/CD Agent                | Pipeline troubleshooting for Jenkins and GitHub Actions                        |
| Architecture Diagram Agent | Generates infrastructure diagrams from AWS and Kubernetes resources            |
| PrivateGPT Agent           | Secure, enterprise ChatGPT-like experience running within your AWS environment |
| Database Explorer Agent    | Safe database queries via pre-approved templates                               |

See the [full list of out-of-the-box agents](https://docs.duplocloud.com/docs/ai-suite/ai-helpdesk/out-of-the-box-agents).

</details>

<details>

<summary>Can we use our own LLM?</summary>

Yes. Dynamic Agents support AWS Bedrock as a first-class LLM provider, with additional providers available. The platform is model-agnostic at the agent level — you can configure each agent to use the model that fits your requirements and data residency constraints.

</details>

## Operations & Reliability

<details>

<summary>Who is responsible for AI's mistakes and how do I protect against them?</summary>

There are two layers of protection:

1. **Deterministic, permission-based controls** — the Scope you assign to an Engineer defines exactly what IAM permissions the agent gets. The platform uses those permissions to generate temporary credentials passed to the agent as part of the ticket. The agent cannot act outside those boundaries regardless of what it's asked to do.
2. **Skills** — best practices and operational guardrails are encoded directly into the agent's Skills. Skills define not just what an agent can do, but how it should do it, including safety checks and approval steps.

DuploCloud's human operations team also acts as a reliability layer — reviewing complex work and stepping in when something requires human judgment.&#x20;

</details>

<details>

<summary>What happens to our data if we stop using DuploCloud?</summary>

Your infrastructure stays in your accounts — Terraform state, Kubernetes manifests, and all provisioned cloud resources remain fully under your control and continue operating. The Knowledge Base and audit trail are your data, stored in your own repositories (generally, as markdown files) and in DuploCloud's vector database, and can be exported at any time. DuploCloud does not own or lock in any of the artifacts produced.&#x20;

</details>

## Integration & Tooling

<details>

<summary>Can you show us some Jenkins agents?</summary>

Yes — DuploCloud has deployed Jenkins agents for multiple customers. The out-of-the-box [CI/CD Agent](https://docs.duplocloud.com/docs/ai-suite/ai-helpdesk/out-of-the-box-agents) supports Jenkins and GitHub Actions pipeline troubleshooting. Please contact the team to arrange a targeted demonstration.

</details>

<details>

<summary>Can we use our existing Terraform, Helm, or other IaC?</summary>

Yes. The platform includes a Terraform Skill out of the box, covering plan, apply, state management, and error handling. Helm and Kubernetes deployments are handled by the Kubernetes Agent and Skills. External Skill packages from HashiCorp and Pulumi can also be made available to the agents. Your existing IaC files, modules, and conventions are used as-is — the agent works with your code, not a replacement for it.&#x20;

</details>

<details>

<summary>How does DuploCloud integrate with our existing CI/CD pipeline?</summary>

Git repositories (GitHub, GitLab, Bitbucket) are modeled as [Providers](introduction/ai-devops-policy-model/providers.md) with scoped access. The out-of-the-box [CI/CD Agent](https://docs.duplocloud.com/docs/ai-suite/ai-helpdesk/out-of-the-box-agents) integrates with Jenkins and GitHub Actions for pipeline troubleshooting and automation. For deeper pipeline integration, custom agents or Skills can be configured to fit your specific workflow.

</details>

## Getting Started

<details>

<summary>How long does it take to get started?</summary>

The platform is designed to be operational quickly. Setup involves deploying a few Docker containers, connecting your cloud and Git providers, and configuring an Engineer with the appropriate Skills and Scopes. All of which can be done in a few minutes, not days.&#x20;

The 30-day PoC is structured to deliver measurable results against real infrastructure within the first sprint. Please contact the team to start scoping your onboarding.

</details>

<details>

<summary>What cloud providers and platforms are supported?</summary>

| Category            | Supported                                                                 |
| ------------------- | ------------------------------------------------------------------------- |
| Cloud               | AWS, GCP, Azure                                                           |
| Kubernetes          | EKS, AKS, GKE, RHOS                                                       |
| Git                 | GitHub, GitLab, Bitbucket                                                 |
| Observability       | OpenTelemetry, Datadog, New Relic, Sentry                                 |
| Incident Management | Grafana Alert Manager, Datadog, New Relic, Sentry, PagerDuty, Incident.io |
| Extended access     | MCP Servers (any system with an MCP endpoint)                             |

See [Providers](introduction/ai-devops-policy-model/providers.md) for the full list and setup instructions.

</details>

<details>

<summary>Do you support self-hosted or on-premise deployments?</summary>

DuploCloud runs within your own cloud environment — your infrastructure, your accounts, your data. The PrivateGPT Agent, for example, uses AWS Bedrock to ensure sensitive data never leaves your AWS environment.&#x20;

For customers with strict data residency or on-premise requirements, contact [support@duplocloud.net](mailto:support@duplocloud.net) to discuss deployment options.

</details>
