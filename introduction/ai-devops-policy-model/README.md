---
description: >-
  A high-level overview of the building blocks of DuploCloud's AI DevOps
  Engineer
---

# AI DevOps Policy Model

The DuploCloud AI DevOps Policy Model lays down the foundational building blocks of the system that orchestrates large and complex DevOps projects seamlessly—just as a human engineer would.&#x20;

The diagram below illustrates this Policy Model.&#x20;

Administrators define access to IT systems by creating providers and supplying the right credentials and scopes. They also create "Workspaces" within which all DevOps work is orchestrated. Workspaces have access to skills via bundles called Personas and have access to the defined Provider scopes.&#x20;

Users are granted access to specific workspaces and can accomplish their tasks within them. For simple one-off tasks, they can create "Tickets" on the HelpDesk and assign the task to an AI agent.  For large and complex work, they can create "Projects" that use a Spec Driven DevOps process.&#x20;



<figure><picture><source srcset="../../.gitbook/assets/Policy_Model_Dark_V2.png" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/duplocloud-diagram-2-light (1).png" alt=""></picture><figcaption></figcaption></figure>

## Core Concepts

Below are brief introductions to the core concepts of the AI DevOps Policy Model, which will be explained in detail in subsequent sections.

### 1. Provider

A Provider is any IT system that you would like Duplo's Platform to access, including cloud platforms (AWS, Azure, GCP), Git repositories, MCP Servers, and more. Each Provider is associated with a specific account or namespace and requires credentials to be provided for authentication. Credentials are safely stored in DuploCloud, enabling just-in-time, scoped access to resources without exposing sensitive authentication data.

### **2. Scope**

Scope defines what the Duplo Platform can access within each Provider. Each Scope entry specifies a Provider and associated Credential, and includes granular access controls through regions, resource types, tags, or custom resource maps (key-value pairs for filtering specific resources like namespaces). Scope can also include MCP Servers for extended system access.

### 3. Agent

The DuploCloud platform includes a DevOps Agent that can perform complex DevOps tasks. It operates within the scopes assigned to it and can inherit skills that extend its capabilities and adapt its behavior to organizational needs. It comes pre-packaged with skills to perform cloud and Kubernetes troubleshooting, project planning and execution, dashboard creation, reporting, etc.

### 4. Skill

A Skill is an instruction or prompt that tells the Duplo Agent how to behave or what capabilities it has. Skills represent the atomic unit of capability within the system. Examples include Kubernetes troubleshooting skills, Terraform provisioning skills, cost optimization skills, and custom skills tailored specifically to an organization's workflows or requirements.&#x20;

### 5. Persona

A Persona serves as a logical container that brings multiple Skills together. Personas help customers organize capabilities by role or function, making it easier to manage and deploy different sets of abilities. For instance, an SRE Persona might combine troubleshooting, monitoring, and incident response skills. Similarly, a Provisioning Persona could bundle Terraform skills with Kubernetes deployment skills, while a Security Persona might group compliance skills with security scanning skills.

### 6. Workspace

A Workspace is where all of this comes together. It's a logical entity to which you can attach any number of Scopes and Personas. You can create multiple Workspaces and invite users to specific Workspaces, thereby creating a separation of responsibilities within the organization. For example, the L1 SRE workspace may have "read-only" access to your infrastructure and codebase, but can have write access to the incident management and observability systems. That workspace would include the SRE Persona with skills for troubleshooting cloud systems and Kubernetes.&#x20;

## Workflow concepts

Below are some of the workflow concepts in the AI DevOps Policy Model:&#x20;

### 1. Project

A Project is a logical entity representing planned work. Each Project must contain a Name, Scopes and Skills. Optionally, it may also have a description, a system prompt, priority, start date and end dates. Think of a Project as a logical container where you can plan and execute large and complex DevOps work. Projects use a Spec Driven DevOps approach.&#x20;

### 2. Spec

A specification, or spec, is the Project document that defines a Project’s goals and requirements in natural language. The user provides high-level requirements, and the agent converts them into a detailed spec. The spec can also include preferences or instructions that guide the agent’s work. Users can edit the document directly or prompt the agent to revise it until they are satisfied.

### 3. Plan

Once the Spec has been finalised, the agent creates a Plan document. It contains a breakdown of how to accomplish the goals specified in the Spec. The requirements are converted into specific tasks and divided into "Phases". A general principle is that the tasks in each phase could be executed in parallel, thereby increasing the speed of project execution. A user can make edits to the plan document directly or by prompting the agent to make changes, until satisfied.&#x20;

### 4. Task

A Task represents a unit of work within a Plan. The Duplo Agent generates Tasks from an approved Plan. Each Task can be converted into a "Ticket" and assigned to a user for execution. Tasks within a Phase can generally be processed in parallel. Users can add new tasks or modify existing ones. When required, the agent will automatically make suitable changes to the spec and plan to include these changes.

### 5. Ticket

A Ticket is a unit of record that stores work performed on the Duplo platform. It is similar to a Jira or Zendesk ticket. All interactions with the Duplo Agent happen within a ticket. You can create standalone tickets for small tasks in the DevOps HelpDesk or create a ticket for each task within a Project. Each ticket has its own scopes and skills that define the boundaries of the work.



{% hint style="info" %}
The following sections explain each concept in more detail and provide guidance for setting them up in your organization.
{% endhint %}

