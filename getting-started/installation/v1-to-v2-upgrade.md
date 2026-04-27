# Helpdesk V1 to V2 Upgrade Guide

This guide covers upgrading from **Helpdesk V1** (the `Duplo.ai.studio` Windows service running on the DuploCloud master VM) to **Helpdesk V2** (a fully Kubernetes-native deployment managed via Helm, running inside a DuploCloud tenant).

---

## What Changes

| | V1 | V2 |
|---|---|---|
| **Deployment** | Windows service on the master VM | Helm chart in a Kubernetes tenant |
| **Infrastructure** | Runs on the master host | Dedicated EKS nodes (ASG) |
| **Storage** | Local disk on master VM | EFS (Elastic File System) |
| **Load balancing** | Front door proxy on master VM | AWS ALB via Kubernetes Ingress |
| **Updates** | Manual service reinstall | `helm upgrade` |
| **Observability** | Windows Event Viewer | Kubernetes pod logs, DuploCloud portal |

V2 runs entirely within your AWS account inside a DuploCloud tenant. V2 is 100% self-hosted — all data remains in your environment.

---

## What's New in V2

| Capability | V1 | V2 |
|---|---|---|
| **AI Agent** | Basic Q&A | Autonomous agent with tool execution |
| **Web Terminal** | Not available | Browser-based terminal for agent commands |
| **MCP Integrations** | Not available | Extensible tool integrations via MCP |
| **Ticket Management** | Basic | Full project and ticket lifecycle management |
| **Multi-provider support** | Single AWS account | Multiple AWS accounts, Kubernetes, Jira, Linear, Slack, and more |
| **Updates** | Manual reinstall required | Single-command Helm chart upgrades |

---

## Upgrade Overview

The upgrade is performed by DuploCloud and consists of the following steps:

1. **Deploy V2** — DuploCloud provisions a new tenant with dedicated EKS nodes and EFS storage, then deploys the V2 Helm chart. A new core platform portal version is also deployed to ensure UI compatibility with V2.
2. **Update the portal routing** — the DuploCloud master portal's front door proxy is updated to route traffic to the new V2 endpoint.
3. **Enable the AI feature flag** — the `ENABLE_AI` flag is enabled in the master portal system settings.
4. **Decommission V1** — the `Duplo.ai.studio` Windows service is stopped and removed from the master VM.
5. **Update DNS** — the portal domain is pointed to the new V2 ALB.

If any issue arises before V1 is decommissioned, the process can be paused — V1 remains fully operational until V2 is confirmed healthy.

---

## What You Need to Provide

DuploCloud already has access to your AWS account and Kubernetes cluster through the existing platform. No additional credentials are needed.

Before scheduling the upgrade, confirm the following:

| Item | Notes |
|---|---|
| Portal domain for V2 Helpdesk | e.g. `helpdesk.yourcompany.com` |
| xterm subdomain | e.g. `xterm.helpdesk.yourcompany.com` |
| Super-user email list | Comma-separated admin emails for initial access |
