# Overview

The Extension Framework lets teams build domain-specific Ops applications on top of the CaaS platform. These applications orchestrate existing tool chains — AWS, Salesforce, ServiceNow — through structured workflows and resource lifecycle management. End users work through forms and structured interfaces; the framework orchestrates the underlying platforms through tickets.

## The Three-Layer Stack

The CaaS architecture is organized in three layers, each building on the one below it.

### Layer 1: CaaS Platform

The foundation layer provides multiplayer ticketing, connectors, workspaces, RBAC, cost management, and tokenless analytics. This is a complete product on its own; teams use it daily for HelpDesk tickets, Projects, dashboards, and cross-role collaboration in shared workspaces.

### Layer 2: Extension Framework

Built directly on top of CaaS, this layer adds domain-specific orchestration: a resource taxonomy, dependency enforcement, multi-step forms, REST APIs, and status lifecycle management. Every capability from the CaaS platform — multiplayer sessions, audit trails, cost tracking, RBAC — is inherited automatically. No rebuild required.

### Layer 3: Developer Experience

A hosted environment where you can build and ship a full Ops application in days, using a web browser or Claude Code with the DuploCloud plugin. DuploCloud hosts the running application, or you can download a Kubernetes manifest and self-host. There is no infrastructure to deploy.

## Why Not Just Use CaaS Directly?

CaaS works well as a general-purpose platform from the start. But as teams begin using it heavily for operational work, a pattern emerges. User needs turn out to be highly repetitive — deploying applications to a cluster, qualifying a sales prospect, troubleshooting a crash — and the underlying structure of each request and response is consistent.

Expressing these workflows in natural language every time becomes laborious. Teams start wanting domain-specific forms, templates, and a consistent policy model for their resources. That is the inflection point where the Extension Framework becomes useful.

## The Policy Model

The policy model is the core concept in the Extension Framework. It is a structured description of the resources your Ops application manages — what they are, what the user provides, what the agent produces, how they relate to each other, and what instructions the agent follows to manage them.

### Resources

Each Ops application manages a taxonomy of domain-specific resources. The taxonomy reflects how the domain is actually organized:

* **DevOps**: Network, Cluster, Environment, Namespace, Workload
* **SalesOps**: Cohort, Account, Qualification, Engagement
* **SecOps**: Policy, Scan, Finding, Remediation

Resources form the navigational structure of the application. Each resource type gets its own list view, detail view, create form, and API endpoint.

### Spec

The spec is what the user provides — a typed input that captures their intent for a resource. For a Network, the spec includes region, VPC CIDR, availability zones, NAT gateway configuration, and subnet prefix. For a Sales Account, it is simply a company name and website. The spec becomes a form in the UI and an API contract for programmatic access.

### Result

The result is what the agent produces — a typed output captured after execution completes. For a Network, the result includes the VPC ID, subnet IDs, security groups, and route tables. For a Sales Account qualification, it includes signal analysis, fit verdict, and extracted leads. The result is stored against the resource and surfaced in a dedicated tab in the detail view.

### Dependencies

Resources form a hierarchy, and the framework enforces it. A Cluster requires a Network. An Engagement requires a Qualification. An Environment lives inside a Cluster. These relationships are declared in the policy model and enforced at every level: the UI shows only valid options at creation time, and the lifecycle respects ordering during provisioning and deprovisioning.

### Skills per Resource Type

Each resource type has a skill associated with it — a set of instructions that tell the agent how to provision, update, troubleshoot, and deprovision that resource. A Network skill might contain a CloudFormation template and tagging policies. A Sales Qualification skill might encode the organization's ICP criteria and web research instructions. Skills are user-owned and user-modifiable, not hardcoded by DuploCloud. If the LLM is capable enough to manage a resource from the spec alone, a skill is optional.

{% hint style="info" %}
For a full description of how skills are structured and managed, see the [Skills](https://github.com/duplocloud/docs/blob/main/introduction/ai-devops-policy-model/skills/README.md) pages in the Introduction section.
{% endhint %}

## What the Framework Provides Automatically

Once you define a policy model and write skills, the framework generates the following without any additional code:

* Multi-step forms with validation for each resource type
* REST APIs for every resource type
* List views with status tracking
* Detail views with Spec and Result tabs
* Automatic ticket creation for every provisioning operation
* Cost tracking per resource
* RBAC inherited from workspaces
* "Track Provisioning Status" links that drop users directly into the underlying ticket
* Multiplayer collaboration and complete audit trails
