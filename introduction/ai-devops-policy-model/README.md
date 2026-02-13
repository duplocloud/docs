---
description: >-
  A high-level overview of the building blocks of DuploCloud's AI DevOps
  Engineer
---

# AI Devops Policy Model

The DuploCloud AI Devops Policy Model lays down the foundational building blocks of the system that orchestrates large and complex DevOps projects seamlessly - just as a human engineer would.&#x20;



This diagram illustrates a hierarchical AI DevOps platform architecture where Admins define permissions and integrations, Engineers are configured with capabilities and boundaries, Projects break down requirements into executable plans and tasks, and specialized Agents handle the actual work through multi-agent orchestration in a ticket-based workflow.<br>

<figure><img src="../../.gitbook/assets/unknown (1).png" alt=""><figcaption></figcaption></figure>



#### Core Concepts

Below is a brief introduction to the core concepts in the Policy Model. These will be explained in detail in subsequent sections:&#x20;



**1. Engineer**

The primary entity representing an AI DevOps Engineer. Each Engineer is defined by several key attributes that govern its behavior and capabilities. It has a unique name within your organization and contains a Persona, which are containers of Skills. The Engineer operates within defined access boundaries called Scope, with specific exceptions managed through Guardrails. As it works, the Engineer builds a Knowledge Base containing learned information about the environment. Resource usage is controlled through Quota settings, and the Engineer's performance is tracked through Health Metrics, which include analytics and cost data.



**2. Skill**

A Skill is an instruction or prompt that tells the agent how to behave or what capabilities it has. Skills represent the atomic unit of capability within the system. Examples include Kubernetes troubleshooting skills, Terraform provisioning skills, cost optimization skills, and custom organization-specific skills tailored to particular workflows or requirements.&#x20;



**3. Persona**

A Persona serves as a logical container that organizes multiple Skills together. Personas help customers organize capabilities by role or function, making it easier to manage and deploy different sets of abilities. For instance, an SRE Persona might combine troubleshooting skills with monitoring skills and incident response skills. Similarly, a Provisioning Persona could bundle Terraform skills with Kubernetes deployment skills, while a Security Persona might group compliance skills with security scanning skills.



**4. Scope**

Scope defines what the Engineer can access within the infrastructure and tooling ecosystem. This includes cloud accounts and namespaces, repositories such as Git and other code or configuration repositories, and MCP servers which provide access to observability tools, SIEM systems, cloud platforms, and DuploCloud MCPs.



**5. Guardrails**

Guardrails define exceptions within the Scope, specifying what the Engineer cannot access or do. These restrictions can target specific resources to exclude, such as a production database instance, specific operations that should be restricted, or specific environments that should be avoided entirely. Guardrails provide fine-grained control over the Engineer's permissions within its broader Scope.



**6. Quota / QoS**

Quota and Quality of Service settings control resource limits for the Engineer. These controls can include maximum concurrent projects, token limits, and cloud resource provisioning limits. The system is designed to accommodate additional options in future versions as requirements evolve.



**7. Knowledge Base**

The Knowledge Base represents the Engineer's learned understanding of the environment. It captures architecture and topology information, relationships between systems, codebase structure, and historical context from completed work. This knowledge is stored both as files in customer repositories in markdown format and in a vector database within DuploCloud, enabling efficient retrieval and reference during operations.

#### **Workflow concepts**

Below are some of the workflow concepts in the AI Devops Policy Model:&#x20;



**1. Project**

A Project is a logical entity representing planned work. Each Project contains a Title and Summary. The heart of a Project is its requirements.  Requirements can be defined in plain english.



**2. Requirements**

This is a user generated document that enumerates the project’s goals and objectives in natural language. Every project will have the user requirements associated with it. The requirements may also specify how a project’s goals are to be accomplished.



**3. Plan**

A Plan represents an execution plan containing tasks. It is an agent-generated breakdown of how to accomplish a Project's Requirements. An Agent derives the Plan from the Requirements, and it requires human approval before execution. Plans are versioned whenever the underlying requirements change, ensuring traceability. If a user rejects a Plan, they can provide feedback for regeneration, allowing iterative refinement until the Plan meets requirements.



**4. Task**

A Task represents a unit of work within a Plan. An Agent generates Tasks from an approved Plan, and each Task is assigned to an Agent based on the required Skill needed to complete it. Tasks require human approval before proceeding and become Tickets upon approval. Users have the flexibility to add new Tasks by providing feedback to the agent and can override Task routing decisions within the Plan if needed.

<br>
