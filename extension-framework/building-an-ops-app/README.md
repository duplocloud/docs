# Building an Ops Application

This guide walks through five steps to define, build, and ship a domain-specific Ops application on the Extension Framework. By the end you will have a fully operational application built on the CaaS platform — with forms, status tracking, AI-powered execution, RBAC, cost management, and audit trails all inherited from the framework. The only work unique to your domain is defining your resource taxonomy and writing the skills that encode your operational expertise.

## What You'll End Up With

A running Ops application where users interact through structured forms and status views rather than freeform conversation. When a user submits a request, the framework creates a provisioning ticket, dispatches it to the AI agent, and tracks the resource through its full lifecycle — from `New` through `Provisioning` to `Ready`. Every operation is multiplayer (colleagues can observe and continue any session), auditable (every agent action is recorded), and cost-tracked (token consumption is attributed per ticket, per workspace). Dependency rules are enforced automatically: a Cluster cannot be created without a Network; an Engagement cannot begin without a completed Qualification. REST APIs for every resource type are generated from your policy model, so programmatic access requires no additional work. The only things you bring are the resource definitions specific to your domain and the skill instructions that tell the agent how to operate on them.

## Prerequisites

- DuploCloud account with the Extension Framework enabled.
- Domain expertise sufficient to define a resource taxonomy and write skill instructions for each resource type.
- Provider credentials for the IT systems your application will orchestrate (cloud accounts, CRM systems, observability platforms, etc.).

## The Five Steps

1. [Define Your Policy Model](step-1-policy-model.md) — declare your resource types, specs, results, and dependencies.
2. [Write Your Skills](step-2-skills.md) — encode your domain expertise as skill instructions for each resource type.
3. [Connect Providers](step-3-providers.md) — register the IT systems your application will orchestrate.
4. [Configure Workspaces](step-4-workspaces.md) — create workspaces, assign scopes and personas, invite users.
5. [Deploy](step-5-deploy.md) — choose hosted by DuploCloud or self-hosted in your own infrastructure.
