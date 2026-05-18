---
description: 'From Automation to Cognition: Architecting an AI-Native DevOps Platform'
---

# The Extension Framework

**The Extension Framework: AI-Native DevOps Automation**

Using the Extension Framework ARMOR turns into a fully featured DevOps platform with structured workflows, forms, APIs, and resource lifecycle management.

## From Runtime to Application

In the previous section, we learned about ARMOR — the multiplayer agent runtime with ticketing, connectors, intelligence, workspaces, RBAC, projects, analytics, and cost management. This is the first module of the product and serves a vast set of use cases by itself. Teams use it to troubleshoot incidents through tickets, execute complex initiatives through projects, build dashboards through tokenless analytics, and collaborate across roles in shared workspaces.

But as teams use ARMOR heavily for DevOps, a pattern emerges. Users’ needs are highly repetitive workflows: deploying applications to a cluster, provisioning a new VPC, troubleshooting pod crashes, setting up CI/CD pipelines, running compliance scans. The work follows the same structure every time.

> ARMOR gives you multiplayer AI-as-a-service. The Extension Framework lets you build **AI-native DevOps applications** on top of it — with structured workflows, resource lifecycle management, forms, APIs, and domain-specific orchestration. Using natural language, without structured workflows, it is not practical to either run daily operations or build automated pipelines

Think of it this way: ARMOR is a platform where users interact with AI through conversations and projects. The Extension Framework lets you build an application where users interact through **forms and structured workflows.**&#x57;orkflows trigger Tickets that use either AI, API or Scripts to accomplish tasks.

## The DuploCloud DevOps Extensions

DuploCloud ships with a **comprehensive, battle-tested set of extensions for Cloud operations** built on the Extension Framework. This is not a starter template or a demo. It is a comprehensive production-grade DevOps platform validated and operational in hundreds of customers, covering the full spectrum of cloud infrastructure operations — from infrastructure provisioning and application deployment through observability, CI/CD, security, and compliance. Multiple compliance standards are implemented out-of-the-box.

The default extension includes coverage across every major DevOps function:

<table><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><p><strong>Deployment</strong> </p><p>Infrastructure provisioning, application deployment, environment management. Networks, clusters, namespaces, workloads, configs, storage.</p></td><td valign="top"><p><strong>CI/CD</strong> </p><p>Build pipelines, deployment automation, release management. GitHub Actions, GitLab CI, Jenkins, ArgoCD.</p></td><td valign="top"><p><strong>Observability</strong> </p><p>Monitoring, logging, alerting, dashboards. Datadog, New Relic, CloudWatch, Prometheus, Grafana.</p></td></tr><tr><td valign="top"></td><td valign="top"></td><td valign="top"></td></tr><tr><td valign="top"><p><strong>Compliance</strong> </p><p>SOC 2, HIPAA, PCI-DSS, ISO 27001. Policy enforcement, evidence collection, audit report generation.</p></td><td valign="top"><p><strong>Security</strong> </p><p>Vulnerability scanning, IAM management, secret rotation, network policy enforcement. SIEM integration.</p></td><td valign="top"><p><strong>Cost Optimization</strong> </p><p>Cloud spend analysis, right-sizing, reserved instance management, budget alerts across AWS, Azure, GCP.</p></td></tr></tbody></table>



Customers adopt the platform in 3 modes:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><p><strong>Use as-is</strong> </p><p>Deploy and start operating immediately. Hundreds of customers run production with out-of-box setup with no changes.</p></td><td valign="top"><p><strong>Customize</strong> </p><p>Fork skills, modify specs, add tagging policies, adjust compliance rules. User-owned — change without waiting for a vendor.</p></td><td valign="top"><p><strong>Build your own</strong> </p><p>Write a completely new extension for any operations function unique to your organization. Build any number of new extensions</p></td></tr></tbody></table>

## How an Extension Works

An extension is a domain-specific application built on top of ARMOR. To build one — or to understand how the default DevOps extension works — you need three concepts:

### 1. The Policy Model

The policy model is a taxonomy of **resources** — the domain-specific objects the application manages. In the DevOps extension, resources mirror how cloud infrastructure is organized:

**Network** → **Cluster** → **Environment** → **Namespace** → **Workloads**

Each resource type defines four things:

| <p><strong>Spec — what the user wants</strong> </p><p>A typed specification capturing intent. For a Cluster: network source, cluster type, EKS version, API visibility, control plane logging. Becomes a form and an API contract.</p> | <p><strong>Result — what was produced</strong> </p><p>A typed output capturing the outcome. For a Cluster: EKS ARN, node groups, endpoint URL, kubeconfig. For an Environment: security groups, IAM roles, KMS keys.</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p><strong>Dependencies — what needs what</strong> </p><p>Resources form a hierarchy. A Cluster requires a Network. An Environment lives inside a Cluster. Dependencies are enforced — the UI shows only valid options.</p>            | <p><strong>Status lifecycle</strong> </p><p>Every resource: New → Provisioning → Ready (or Failed, Blocked). Updates trigger reconciliation. Deletes trigger deprovisioning. Framework manages state transitions.</p>    |

### 2. Skills for Each Resource Type

Each resource type has skills — the instructions that tell the AI agent how to provision, update, troubleshoot, and deprovision that resource. A Network skill might contain a CloudFormation template. A Cluster skill might contain EKS provisioning scripts. The skill is the business logic — user-owned, not vendor-hardcoded.

### 3. The Framework Does the Rest

Once resources and skills are defined, ARMOR provides everything else automatically: multi-step forms with validation, REST APIs for every resource type, list views with status tracking, detail views with Spec/Result tabs, automatic ticket creation, cost tracking per resource, RBAC inherited from workspaces, and “Track Provisioning Status” links to the underlying ticket.

_Define your resources and their taxonomy. Write your skills. The platform gives you a fully featured enterprise DevOps application — complete with RBAC, workspaces, determinism, analytics, cost management, centralized context, alerts, notifications, and fault tolerance._

## The Resource Lifecycle

Every resource in the Extension Framework follows the same lifecycle:

![](<../.gitbook/assets/Unknown image (2)>)

_The resource lifecycle: user submits spec, platform creates ticket, agent executes, writes results, resource goes live._

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>1</strong></td><td><p><strong>User submits a spec</strong></p><p>Through the UI form or API — name, scope (which cloud account), optional skill overrides, and domain-specific fields.</p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>2</strong></td><td><strong>Framework creates a ticket</strong><br>Automatically creates a ticket in the user’s workspace. Attaches credentials, resolves skills, writes the spec as JSON to the shared file system.</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>3</strong></td><td><strong>Agent executes</strong><br>Reads the spec and skill instructions, provisions the EKS cluster, configures node groups, sets up IAM roles. The user watches live on the ticket.</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>4</strong></td><td><strong>Agent writes results</strong><br>Writes a structured output file. The framework parses it into the resource’s typed Result and updates the status.</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>5</strong></td><td><strong>Resource is live</strong><br>Spec tab, Result tab, status badge, timestamps, and “Track Provisioning Status” link to the underlying ticket.</td></tr></tbody></table>

**Updates and Reconciliation**\
When a user modifies a spec, the framework sends a reconciliation message. The agent handles the delta — no full teardown and rebuild.

**Deprovisioning**\
When a user deletes a resource, the agent handles cleanup. Dependencies are respected — you can’t delete a Network while Clusters depend on it.

### Example Workflows in the DuploCloud DevOps Extension

The following examples illustrate how the Extension Framework delivers a traditional enterprise application experience — forms, status tracking, dependency chains — while AI handles all the heavy lifting underneath.

### Example: Creating a Cluster with Dependency Enforcement

The cluster creation form demonstrates the dependency chain in action. The “Network Source” field offers two options: “Choose Network” (select from provisioned networks — region, VPC, and subnets inherited automatically) or “Choose VPC” (manual entry). The framework enforces that a cluster cannot be created without a network.

The spec captures everything the agent needs: network source, cluster type, EKS version, API server visibility, control plane logging, and cluster IP CIDR. The user clicks “Create & Provision” and the system creates a provisioning ticket. The agent provisions the entire EKS cluster in real time.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p><em>Completed network — VPC ID, CIDR, Region, Internet Gateway, Subnets and Routing tabs. Status: Ready.</em></p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (70).png" alt=""><figcaption><p><em>Cluster creation form — Network Source shows the dependency chain.</em></p></figcaption></figure>



### Example: Navigating an Environment

Once a cluster is provisioned, teams create environments inside it. The environment is the deployment boundary — containing security groups, IAM roles, and KMS keys.

The environment detail view shows the full resource tree in the left navigation: Overview, Micro Services, Kubernetes (Namespaces, Nodes, Workloads, Configs, Storage, Networks), and Cloud Resources (Hosts, Serverless, Storage, Databases, Networks, Configs). Each sub-resource has its own list view, create form, and detail view. Spec/Result tabs are available throughout. A “Track Provisioning Status” button links to the underlying ticket.

<figure><img src="../.gitbook/assets/image (132).png" alt=""><figcaption><p><em>Full resource tree in the left nav. Security groups, IAM roles, KMS keys in the overview. Spec/Result tabs. Track Provisioning Status links to the underlying ticket.</em></p></figcaption></figure>

This is the pattern at work. The user fills out a form. The framework creates a ticket. The agent provisions the infrastructure. The user sees the result in a familiar enterprise UI. Every operation is multiplayer, auditable, and cost-tracked.

### Skills in Action

The DevOps extension ships with platform skills like _duplo-aws-infra_ that contain CloudFormation templates, IAM policies, security group rules, and provisioning scripts. Users can view these skill files directly from the ticket. Because skills are user-modifiable, an organization can fork a platform skill and customize it — adding their own tagging policies, compliance requirements, or architectural standards — without waiting for DuploCloud to ship an update.

## Extending Beyond the Default

The default DevOps extension is comprehensive — but it’s not the ceiling. The Extension Framework is designed so that organizations can extend the platform in two ways:

### Customize the Default Extension

Every skill in the default extension is user-modifiable. Organizations routinely customize the platform: adding custom tagging policies, modifying network topologies for their multi-account strategy, adding compliance guardrails specific to their regulatory environment, or integrating with internal tools. Customizations are persistent — they survive platform upgrades because the skill layer is separated from the framework.

### Build New Extensions

Organizations can also build entirely new extensions that sit alongside the default DevOps extension on the same ARMOR runtime. A platform team might build an extension for their internal developer platform. A security team might build one for vulnerability management. A data engineering team might build one for ML pipeline orchestration.

Each extension defines its own resource taxonomy, skills, and workflows — but shares the same ARMOR runtime underneath. Workspaces, RBAC, cost management, ticketing, context — all inherited. A single DuploCloud deployment can run multiple extensions simultaneously.

> The default DevOps extension gives you a production-ready platform on day one. Customization gives you flexibility to match your standards. And the ability to build new extensions means the platform grows with your needs — **without waiting for any vendor’s roadmap**.

#### What This Means

**A production-ready platform** The default DevOps extension is comprehensive and battle-tested across hundreds of customers. Deploy it and start operating production infrastructure on day one.

**Complete customizability** Fork any skill, modify any resource spec, add any workflow. The platform adapts to your organization’s specific standards, policies, and architectural patterns.

**Unlimited extensibility** Build entirely new extensions for any operations function. The same framework that powers cloud infrastructure provisioning can power your internal developer platform, compliance automation, or any other structured operational workflow.

{% hint style="info" %}
_DuploCloud doesn’t ship one rigid DevOps tool. It ships a comprehensive, battle-tested DevOps platform — and gives you the framework to extend it in any direction your organization needs._
{% endhint %}

#### What’s Next

ARMOR provides the runtime. Extensions provide the applications. But building and deploying extensions should be as easy as the applications they create.

