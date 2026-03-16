---
description: >-
  If your question isn't answered here, reach out to the team at
  support@duplocloud.com or contact us on Slack.
---

# FAQs

## Getting Started

<details>

<summary>What does DuploCloud's infrastructure look like at a high level?</summary>

DuploCloud runs within your own cloud account. The platform itself is a small footprint — a few Docker containers, a MongoDB instance, and a few S3 buckets.

The product has three main layers:

1. **Engineer Hub** — where you create and manage your AI DevOps Engineers (Platform Engineers, CI/CD Engineers, SRE Engineers, and more). You define high-level project requirements here; the Engineer converts them into a detailed plan and coordinates a team of agents to execute it.
2. **Agentic AI Helpdesk** — the work surface for task-level objectives. Accessible via web browser, Slack, Teams, or directly in an IDE, this is where tickets are created, assigned to specialized agents, and completed. Agents include SRE, Kubernetes, cloud-specific, Docs, and Architecture agents.
3. **Integrations** — the connectivity layer that links agents to your actual infrastructure through cloud providers (AWS, GCP, Azure), Kubernetes clusters (EKS, AKS, GKE), Git repositories (GitHub, GitLab, Bitbucket), observability tools, and MCP servers. Access is granted through Providers and Scopes, with temporary just-in-time credentials passed to agents at execution time.

Your existing infrastructure — Terraform state, Kubernetes clusters, CI/CD pipelines — is not migrated or replaced. Agents connect to it through the integrations layer using the permissions you define.

</details>

<details>

<summary>What makes DuploCloud different from using Claude Code or similar AI coding tools?</summary>

DuploCloud is a multi-agent platform, not a single-user coding assistant. The key differences:

**1. Shared system of intelligence — context doesn't live on individual laptops**
With Claude Code or Cursor, every session starts from scratch. Work done by one engineer isn't visible to teammates, investigations can't be handed off mid-task, and the same context has to be re-established every time. DuploCloud centralises this: every ticket, investigation, and outcome is stored in a shared knowledge base. The second time a similar task runs — a migration, a compliance check, a cluster upgrade — the agent already knows your environment and asks significantly fewer questions.

**2. Team collaboration and handoff**
A task started by one engineer can be continued by another without losing context. Projects, tickets, and plans are visible across the team in a shared workspace, and agents can work in parallel across team members' tasks simultaneously.

**3. Scale and security — credentials managed centrally, not tied to individual laptops**
DuploCloud manages credentials at the platform level, generating scoped, temporary access per ticket. Because the platform runs in your cloud rather than on a developer's laptop, it isn't constrained by local machine availability, access, or session limits. Agents are also restricted to the specific repositories and cloud accounts defined in the Scope for that task — they cannot reach outside their boundaries to gather context, which is a common failure mode with local AI tools.

**4. Always-on, not session-bound**
A long-running task continues after hours, results are surfaced when complete, and the system keeps working while the team is offline.

If your team already uses Claude Code or Cursor for local development, DuploCloud acts as the coordination and record-keeping layer on top — making individual AI work visible, auditable, and collaborative at the team level.

</details>

<details>

<summary>We already have DevOps engineers. Why would we use DuploCloud?</summary>

The same reason companies with thousands of software engineers still give every developer Claude Code or Cursor: AI tools act as a force multiplier, not a replacement. Your engineers direct the work; DuploCloud's AI handles the repetitive and time-consuming parts — routine infrastructure tickets, compliance evidence collection, PR reviews, EKS optimisation passes, cost analysis — so your team can focus on higher-leverage work.

For teams with lean or overloaded DevOps functions, this means eliminating the intake ticket backlog and reducing context-switching. For larger teams, it means running complex projects in parallel rather than sequentially, and removing single points of failure when engineers are unavailable.

DuploCloud also handles work that falls between the cracks of typical DevOps tooling: tribal knowledge documentation, cross-environment compliance scanning, and ongoing infrastructure hygiene — work that's important but rarely urgent enough to get prioritised.

</details>

<details>

<summary>Is DuploCloud similar to Heroku in terms of simplicity?</summary>

Yes — the ease of use is comparable. Teams often start on Heroku for its simplicity and move to AWS for production scale; DuploCloud is designed to give you Heroku-like simplicity on top of AWS (and GCP and Azure), without the cost and limitations of Heroku at scale.

The main differences: DuploCloud gives you access to the full breadth of cloud-native services that Heroku abstracts away, and DuploCloud plus your cloud provider is generally significantly more cost-effective at higher traffic volumes. The added flexibility does introduce some complexity, but DuploCloud's support and AI agents are there to absorb that complexity rather than pass it to your team.

</details>

<details>

<summary>How long does it take to get started?</summary>

The platform is designed to be operational quickly. Setup involves deploying a few Docker containers, connecting your cloud and Git providers, and configuring an Engineer with the appropriate Skills and Scopes. All of which can be done in a few minutes, not days.&#x20;

The 30-day PoC is structured to deliver measurable results against real infrastructure within the first sprint. Please contact the team to start scoping your onboarding.

</details>

<details>

<summary>What does DuploCloud set up for us during onboarding?</summary>

DuploCloud's team handles the initial platform setup as part of onboarding. This includes deploying the platform to your cloud environment, connecting your cloud and Git providers, and configuring your first Engineers with personas, Skills, Scopes, and MCP server integrations for your ticketing and observability tools.

The overall onboarding flow follows the same structure as before — dev deployment, evaluation, QA, production cutover — but the project plan is now managed inside the product rather than a spreadsheet, so your team can track and collaborate on it in real time.

The team will also configure Skills to reflect your code conventions and operational standards before handoff, so agents are working to your patterns from day one.

</details>

<details>

<summary>Does deploying DuploCloud change or disrupt our existing infrastructure?</summary>

No. DuploCloud deploys as a small set of containers inside your existing cloud account — it connects to your infrastructure rather than replacing it. Your Terraform state, Kubernetes manifests, CI/CD pipelines, and running workloads are not touched during onboarding.

If you choose to stop using DuploCloud, your infrastructure continues running exactly as it was; nothing is locked in.

Onboarding typically requires about one meeting per week from your side — DuploCloud's team handles the setup, configuration, and integration work.

</details>

<details>

<summary>Can DuploCloud scan our existing infrastructure and identify what still needs to be done?</summary>

Yes — this is the standard starting point for any project. When you create a Project Plan, you provide the platform with access to your Git repositories and cloud accounts (via Scopes). The planning phase scans what already exists and generates tasks only for what's missing or non-compliant with the target spec.

If you're partway through a migration, the agent picks up from where your team left off — assessing the current state, identifying the remaining gaps, and producing a prioritized task list with code reviews for each delta. You don't start from scratch.

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

<details>

<summary>How are updates and security patches delivered for self-hosted deployments?</summary>

Updates are delivered as new Helm chart versions and Docker image tags. The platform consists of 3–4 containers — updating means pulling the new images and running a Helm upgrade, with no data migration required in typical releases.

DuploCloud maintains a regular release cadence and notifies customers when updates are available. Security patches are released on an accelerated schedule as needed. Because the platform is self-hosted, you control the timing of all updates — nothing is applied to your environment automatically.

For teams who want automated update management, the platform can be configured to watch for new image tags and apply updates through your existing CD pipeline or GitOps workflow.

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

<summary>Is agent memory persistent, and can it be shared across agents?</summary>

Agents themselves are stateless — each execution starts fresh with the context provided in the ticket. Persistence lives at the help desk layer: every ticket maintains a full history of the investigation, actions taken, and outcomes. This history is stored in the Engineer's Knowledge Base and is accessible to any agent working on related tickets.

The result is shared, searchable memory at the system level without individual agents needing to carry state between runs. Agents working on a follow-up ticket can query prior work, and human team members can review or build on the full investigation history.

</details>

<details>

<summary>How do you give AI agents context?</summary>

Context is assembled from four layers and delivered to the agent as part of each ticket:

1. **Graph database** — DuploCloud maintains a graph of your infrastructure that captures relationships between hosts, services, pods, dependencies, and cloud resources — giving agents a structured, queryable map of your environment rather than just flat text.
2. **Knowledge Base retrieval** — the platform uses vector search over the Engineer's Knowledge Base (previous tickets, runbooks, architecture notes) to pull relevant prior work into the prompt.
3. **Skills** — best practices, guardrails, and operational patterns are encoded as Skills and included in the agent's system prompt. This is how domain expertise is consistently applied without relying on the model to infer it.
4. **Scope credentials** — the agent receives temporary, just-in-time credentials scoped to the exact resources it's permitted to access, so it has the access it needs without ever needing to ask for it.

The result is a multi-layer context strategy: graph relationships for infrastructure awareness, vector retrieval for institutional knowledge, Skills for operational expertise, and Scopes for safe execution.

</details>

<details>

<summary>Does the agent ask clarifying questions when a task is underspecified?</summary>

Yes — this is built into the Project flow. When you create a Project, the first step is a Spec: the agent interviews you, surfaces the configuration decisions that matter, and drafts a structured description of what it understands you want before doing anything.

The spec phase exists precisely for the "I don't know what I don't know" problem — it prompts for choices you might not have thought to specify (retention policies, failover behaviour, access patterns, environment boundaries) rather than silently assuming defaults. Once you've reviewed and confirmed the spec, the agent generates a detailed plan and task list for your approval before any execution begins.

On the first run of a new task type, the agent asks more questions to understand your environment and preferences. On subsequent similar tasks, it asks significantly fewer — the knowledge base retains what it learned about your setup, so you're not re-explaining your conventions from scratch each time.

For one-off Help Desk tickets, the agent works with the context it has and follows up inline if clarification is needed before taking an action.

</details>

<details>

<summary>Does DuploCloud's AI actually execute tasks, or does it just give recommendations?</summary>

It executes. When assigned a ticket, DuploCloud's agents run real commands against your infrastructure — `kubectl` operations, AWS CLI calls, Terraform plans and applies — and surface the results for your review before any changes are committed.

The workflow is: the agent takes action, produces a diff or output, and presents it with an explanation. You approve or reject before anything is applied. For example, an EKS cost optimisation ticket might result in the agent analysing 12 nodes, identifying memory and CPU inefficiencies across workloads, and proposing specific resource adjustments — all executable in one click after your review.

This is different from advisory tools that generate recommendations you implement manually. The work happens inside DuploCloud, with a human in the approval loop.

</details>

<details>

<summary>Why use specialized personas rather than one agent with all skills?</summary>

A single agent with all skills would have a very broad system prompt — which degrades LLM performance. Smaller, focused context windows produce more accurate and reliable outputs than large, all-encompassing ones.

Specialized personas also make it easier to enforce security boundaries. An agent scoped to Kubernetes operations has no access to your Git credentials or AWS account — it can only do what its Scope allows. Mixing all capabilities into one agent would require broader permissions and increase the blast radius of any mistake.

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

<summary>Can AI agents assist with compliance evidence collection and audit preparation?</summary>

Yes — this is one of the platform's core use cases. Agents can run scheduled compliance checks across your cloud environments and produce structured evidence artifacts automatically.

Specific capabilities include:
- Cross-account scans against compliance controls (SOC 2, HITRUST, ISO 27001)
- Continuous drift detection: agents flag resources that fall out of compliance between audit cycles, rather than discovering gaps at audit time
- Evidence packaging for auditor review, drawn from ticket history, logs, and live environment state
- GRC platform integration: agents keep controls green in platforms like Drata and Vanta by flagging issues as they arise
- Persistent runbooks and control attestation in the knowledge base, making each subsequent audit cycle faster

Agents operate with read-only scope by default. Remediation actions require explicit human approval before execution — the platform notifies; it does not auto-remediate.

For teams who want DuploCloud to take accountability for compliance outcomes — evidence collection, ongoing control monitoring, and auditor liaison — this is available as a managed service.

</details>

<details>

<summary>Are the prebuilt agents and skills built only by DuploCloud, or can others contribute?</summary>

Prebuilt agents and skills are developed and maintained by DuploCloud, in close collaboration with customers and partners. They are not community-sourced in the open-source sense — this means every skill ships with a quality bar and has been validated against real workloads.

That said, the platform is fully extensible. You can build your own skills, modify existing ones, or use skills published by third-party vendors. For example, Hashicorp publishes a Terraform skill that you can plug directly into your agents.

</details>

<details>

<summary>How much work is it to set up and maintain agents and skills?</summary>

Initial setup is handled by DuploCloud's team as part of onboarding — Engineers, personas, Skills, and Scopes are configured against your environment before you run your first task.

Ongoing maintenance depends on which service model you choose:

- **Fully managed** — DuploCloud's operations team owns the agents, keeps Skills updated, and is accountable for task outcomes. You direct the work (priorities, what to tackle next); the team handles the rest.
- **Hybrid** — your team runs day-to-day tasks, with DuploCloud available for complex or sensitive work.
- **Self-serve** — your team owns configuration and upkeep. Prebuilt agents and Skills are maintained by DuploCloud and require no ongoing effort from you, but custom agents you build yourself are your responsibility.

Skills encode their logic as explicit, versioned instructions — not trained weights. Updating a Skill means editing text, not retraining a model. Prebuilt Skills don't accumulate drift over time.

</details>

<details>

<summary>Can we automate our existing runbooks and release processes?</summary>

Yes — this is a direct use case. Documented processes (release checklists, hotfix procedures, incident runbooks) can be converted into Skills, which agents execute step-by-step with the same guardrails applied to any other task: scoped credentials, human approval before execution, and a full audit trail.

The conversion is straightforward: your runbook becomes a structured Skill that the agent follows. On a release trigger, the agent works through the steps, surfaces any exceptions or decisions that require human input, and completes the process. Engineers stay in the loop without needing to run every command themselves.

For teams running hotfixes and deployments every few days with a manual process, this is typically one of the first workflows automated after onboarding.

</details>

<details>

<summary>Can we use our own LLM?</summary>

Yes. Dynamic Agents support AWS Bedrock as a first-class LLM provider, with additional providers available. The platform is model-agnostic at the agent level — you can configure each agent to use the model that fits your requirements and data residency constraints.

</details>

<details>

<summary>What AI back-ends does DuploCloud use, and why?</summary>

DuploCloud works with managed LLM services from major cloud providers — AWS Bedrock, GCP Vertex AI, and Azure AI Foundry, for example — depending on your cloud environment. Using managed services means your data stays within your own cloud account and is not used to train third-party models. This is important for enterprise security and compliance requirements.

The platform is model-agnostic at the agent level. DuploCloud's team continuously evaluates new models as they are released and updates default model assignments based on what performs best for each task type — reasoning-heavy tasks like Terraform plan analysis may use a different model than higher-volume tasks like log summarisation. Customers can always override the default and choose specific models for specific agents.

</details>

<details>

<summary>Does my choice of container platform affect the quality of AI output?</summary>

In practice, yes. LLMs perform better against widely adopted, open-standard platforms — such as Kubernetes (EKS, GKE, AKS) — than against proprietary or less common orchestration systems. This is because the volume of public documentation, community discussion, and training data is significantly higher for Kubernetes than for alternatives like ECS.

This doesn't mean proprietary platforms aren't supported — they are. But for complex tasks like troubleshooting, cost optimisation, and infrastructure generation, you'll typically get more accurate and detailed output on Kubernetes-based environments.

If you're choosing between platforms and AI-assisted operations is a priority, DuploCloud will factor this into its recommendation during the scoping phase.

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

<summary>Will AI-generated code follow our internal conventions and patterns?</summary>

Yes. Two mechanisms ensure this:

1. **Repository access** — agents with access to your infrastructure repository read your existing code before generating anything new. They infer your naming conventions, module structure, and organisational patterns and apply them to new output rather than falling back on generic defaults.

2. **Skills** — you can explicitly encode your standards as a Skill (module naming conventions, required tags, resource organisation patterns). Skills are included in the agent's system prompt and applied consistently to every task regardless of who initiates it.

For Terraform specifically, agents generate code within your existing directory structure and variable conventions. If the agent is uncertain about a convention, it surfaces the decision in the spec or plan phase for you to confirm before generating any code.

Code review is part of the standard workflow. The platform presents the diff in the ticket interface alongside the agent's reasoning before any changes are applied — you're never committed to output you haven't reviewed.

</details>

<details>

<summary>Does DuploCloud support GitOps workflows (Flux, ArgoCD)?</summary>

Yes. Custom agents and Skills can be built for GitOps tools like Flux and ArgoCD. The platform's core model — agents operating on your Git repositories with scoped access and a full audit trail of proposed changes — maps naturally to GitOps pull-based delivery.

A GitOps-focused agent can manage Flux Kustomizations, HelmReleases, and GitRepository resources alongside your existing reconciliation workflow. Contact the team to scope a custom agent for your GitOps environment.

</details>

<details>

<summary>How does DuploCloud handle Terraform variable management across environments?</summary>

Terraform variable management is addressed at three levels:

1. **System of record** — variables and configuration are backed by your Git repositories. The platform treats your existing repo structure as the source of truth and works within it rather than replacing it.
2. **Scope-based access control** — each environment (dev, staging, production) is modeled as a separate Scope with its own credentials and boundaries. Engineers only access the variables relevant to the Scope they're operating in, preventing cross-environment leakage.
3. **Skills** — Terraform Skills encode best practices for module structure, variable organization, and environment promotion patterns, ensuring consistency across environments regardless of which team member or agent is making changes.

If you're partway through a migration, the platform can scan your existing repositories and cloud accounts to identify gaps and generate a remediation plan.

</details>

<details>

<summary>How does DuploCloud integrate with our existing CI/CD pipeline?</summary>

Git repositories (GitHub, GitLab, Bitbucket) are modeled as [Providers](introduction/ai-devops-policy-model/providers.md) with scoped access. The out-of-the-box [CI/CD Agent](https://docs.duplocloud.com/docs/ai-suite/ai-helpdesk/out-of-the-box-agents) integrates with Jenkins and GitHub Actions for pipeline troubleshooting and automation. For deeper pipeline integration, custom agents or Skills can be configured to fit your specific workflow.

</details>

<details>

<summary>We already use Drata, Vanta, or Thoropass. Does DuploCloud replace them?</summary>

No — they're complementary. GRC platforms like Drata, Vanta, and Thoropass identify compliance gaps and manage the audit workflow. DuploCloud does the technical work to close those gaps: building controls into your infrastructure, remediating findings, and keeping them green as your environment evolves.

A common pattern: your GRC platform flags a control as failing; DuploCloud's agents identify the root cause, propose a remediation, and execute it after your approval. DuploCloud integrates directly with GRC platforms to keep control statuses current.

</details>

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

<summary>What if a user accidentally pastes credentials or secrets into a prompt?</summary>

DuploCloud applies a security validation Skill to all agents. When an agent detects that a prompt contains patterns consistent with secrets — API keys, access tokens, passwords, or cloud provider credentials — it refuses to process the request and returns a warning explaining why.

More broadly, the platform is designed so that users never need to supply credentials in prompts at all. Credentials are managed at the Scope level and injected as temporary, just-in-time credentials at execution time. If a user tries to bypass this by pasting credentials directly, the security Skill acts as a catch.

For stronger guarantees, Scopes can be configured to remove sensitive credential access from the user-facing layer entirely — the agent simply doesn't have the access to misuse.

</details>

<details>

<summary>What compliance certifications does DuploCloud have?</summary>

DuploCloud is SOC 2 certified. Full security documentation is available for procurement review. The platform is used by customers in regulated industries including fintech and healthcare. Contact [support@duplocloud.net](mailto:support@duplocloud.net) for compliance documentation.

</details>

<details>

<summary>Does DuploCloud provide SOC 2 certification or conduct security audits?</summary>

No — DuploCloud is not an auditor and does not issue certifications. What DuploCloud does is ensure your infrastructure meets SOC 2, HIPAA, HITRUST, PCI, and other framework requirements on an ongoing basis: compliance controls are built directly into every deployment, agents continuously scan for drift, and evidence is collected and packaged automatically for auditor review.

When you're ready for formal attestation, you engage a qualified auditor directly (or through your GRC platform). DuploCloud can connect you with auditors and provides the infrastructure evidence and control documentation they need.

Penetration testing is available as a DuploCloud service offering, which is typically the final step before audit submission.

</details>

<details>

<summary>Does the AI agent collect data in any capacity?</summary>

No. Agents only access metrics and logs from within your own cloud account, and only with your approval before any action is taken. No data leaves your account, and no data collection occurs beyond what is needed to respond to your request.

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

<summary>Can AI agents be trusted to make compliance decisions, or does human judgment still have a role?</summary>

For technically deterministic compliance work — scanning environments for misconfigurations, collecting evidence against a control, verifying that a resource meets a specific policy — agents perform reliably and can run autonomously within their defined Scope.

For judgment-heavy decisions — interpreting ambiguous regulatory requirements, determining whether a specific implementation satisfies a regulator's intent, or navigating evolving frameworks like the EU AI Act or global data privacy laws — human expertise remains essential. The platform is built around this distinction: agents propose findings and actions, humans review and approve before anything is executed. DuploCloud's human operations team is available throughout for guidance on implementation decisions, not just execution.

Three layers apply to every agent action:
1. **Scoped access** — agents receive only the IAM permissions defined in the ticket's Scope and cannot act outside those boundaries.
2. **Skills** — compliance patterns and guardrails are encoded as Skills and applied consistently, independent of model inference.
3. **Human approvals** — changes to infrastructure or configuration require explicit sign-off before execution.

The practical model: agents automate evidence collection, continuous monitoring, and remediation recommendations; humans review what those findings mean and decide what to do about them.

</details>

<details>

<summary>How do LLM model updates work, and will they affect my agents?</summary>

DuploCloud is model-agnostic. Each agent is configured to use a specific model through your cloud provider's managed LLM service (e.g., AWS Bedrock, Azure OpenAI), which you control. Model updates are not applied automatically — you decide when to change the model an agent uses.

DuploCloud monitors model performance across its customer base and makes recommendations when a newer model produces meaningfully better results for a specific task type (e.g., Kubernetes operations, Terraform plan analysis). These are recommendations, not forced updates.

Because Skills encode best practices as explicit, versioned instructions, agent behavior remains consistent even as underlying models evolve — the guardrails don't change with the model.

</details>

<details>

<summary>What happens to our data if we stop using DuploCloud?</summary>

Your infrastructure stays in your accounts — Terraform state, Kubernetes manifests, and all provisioned cloud resources remain fully under your control and continue operating. The Knowledge Base and audit trail are your data, stored in your own repositories (generally, as markdown files) and in DuploCloud's vector database, and can be exported at any time. DuploCloud does not own or lock in any of the artifacts produced.&#x20;

</details>

<details>

<summary>How does DuploCloud help with cloud cost visibility and unexpected cost increases?</summary>

DuploCloud agents can audit your cloud environment for common cost drivers — unused or oversized resources, missing VPC endpoints generating data egress charges, untagged infrastructure with no cost attribution, and instances left running after workloads moved to managed services.

Cost savings are attributed to specific tickets in the audit trail, giving you a clear record of what was changed and why.

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

<details>

<summary>Does DuploCloud track ROI metrics — tickets resolved, PRs generated, time saved?</summary>

Activity is tracked at the ticket level — every completed task records what was done, what commands were executed, what changes were proposed and approved, and how long it took. This data is queryable via the Analytics Agent: you ask in natural language and it queries project history directly, answering questions like "how many tickets were completed this sprint," "what was the infrastructure cost delta over this project," or "how does AI-assisted throughput compare to estimated manual effort."

An analytics dashboard is on the roadmap. Agent-level observability is already built in: all agents emit OpenTelemetry traces and metrics (latency, failure rates, success rates) to your cloud's monitoring stack (e.g., AWS X-Ray), enabling benchmarking of individual agent performance over time.

For PoC engagements, the team can structure the evaluation around specific KPIs — establishing a baseline before the PoC starts and measuring against it at the end. A common methodology is comparing the token cost and human oversight time for a given project done with distributed local AI tools against the same project run centrally through DuploCloud.

</details>
