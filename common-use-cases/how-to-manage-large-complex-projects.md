# DuploCloud AI DevOps — End-to-End Demo

This walkthrough demonstrates how DuploCloud's AI DevOps suite takes an existing e-commerce order service running on AWS EKS from zero observability and security hardening to a fully production-ready, SOC 2-compliant platform — in a single automated workflow.

---

## The Starting Point

A simple order service is deployed in a sandbox environment. The goal: scale the platform and pass a SOC 2 audit in 90 days. The microservice architecture runs 5–10 services on AWS EKS with no observability, no cost controls, no automated pipelines, and no security hardening.

![Demo overview](../.gitbook/assets/demo-01-overview.png)

---

## Step 1 — Connect the Service to DuploCloud

Before any work can begin, the service must be connected to DuploCloud. Providers and scopes for both AWS and Kubernetes have already been created.

**Verify AWS Connection** — An AWS provider is configured with the correct credentials and scope. Confirming the sandbox nodes are running verifies DuploCloud is connected to the AWS account.

![AWS sandbox nodes running](../.gitbook/assets/demo-03-aws-nodes-running.png)

**Verify Kubernetes Connection** — A Kubernetes provider is configured with credentials and a scope defining what DuploCloud can access. Confirming the pods from the order service are visible verifies the connection.

![Pods running](../.gitbook/assets/demo-05-pods-running.png)

---

## Step 2 — Set Up the Workspace

All work inside DuploCloud happens inside **workspaces**. Select the workspace for this project — it already has the required skills and agents configured.

![Workspaces](../.gitbook/assets/demo-06-workspaces.png)

Scroll down to **Cloud Providers** and add the new scope for the service. Then under **Kubernetes**, add the scope that gives the system access to this particular service. Hit **Update** to save.

![Adding scopes to workspace](../.gitbook/assets/demo-07-adding-scopes-to-workspace.png)

![Update workspace](../.gitbook/assets/demo-08-update-workspace.png)

---

## Step 3 — Create a Project

Navigate to **AI DevOps → Projects**. Create a new project, give it a name, and select the right scopes and skills. DuploCloud uses a **spec-driven approach** (as recommended by Anthropic) — open the **AI Planner** and provide a prompt with all project requirements.

![Create new project](../.gitbook/assets/demo-09-create-project.png)

![AI Planner with requirements prompt](../.gitbook/assets/demo-10-ai-planner-prompt.png)

DuploCloud runs a **discovery process**, asking for user input where required.

![Discovery process running](../.gitbook/assets/demo-11-discovery-process.png)

Once complete, it produces a **spec document** with high-level requirements, then a **plan document** with the step-by-step process divided into phases and tasks, and finally a list of **execution tasks** divided into stages.

![Spec document](../.gitbook/assets/demo-12-spec-document.png)

![Plan document](../.gitbook/assets/demo-13-plan-document.png)

![Execution tasks by stage](../.gitbook/assets/demo-14-execution-tasks.png)

> **Tip:** Save the spec, plan, and execution task files — Claude Code can use them as context when picking up tasks directly in your IDE.

---

## Step 4 — Project Dashboard and Tickets

Back on the project dashboard, the agent has created **individual tickets** for each task, grouped by phase.

![Project dashboard with tickets](../.gitbook/assets/demo-15-project-dashboard-tickets.png)

![Phases with tickets](../.gitbook/assets/demo-16-phases-with-tickets.png)

---

## Step 5 — Execute the First Task

Open the first ticket to find the current state — the metrics server is not installed and no metrics are reporting. DuploCloud works autonomously, installs the metrics server, and metrics are now being reported.

![First task ticket open](../.gitbook/assets/demo-17-first-task-ticket.png)

![Metrics server missing](../.gitbook/assets/demo-18-metrics-server-missing.png)

![Metrics now reporting](../.gitbook/assets/demo-19-metrics-reporting.png)

---

## Step 6 — Collaborate via Claude Code

The next task is assigned to a team member (John) who prefers working from his IDE using DuploCloud's **Claude Code plugin**. He initializes the workspace and project and picks up right where the team left off.

![John using Claude Code plugin in IDE](../.gitbook/assets/demo-21-ide-claude-code-plugin.png)

John executes two tickets via Terraform — enabling EKS control plane logging to CloudWatch, then enabling Container Insights to collect pod-level metrics via a CloudWatch agent daemon set.

![Container Insights Terraform change](../.gitbook/assets/demo-22-container-insights-terraform.png)

Everything done in Claude Code is automatically mirrored back in the ticket.

![Changes mirrored in ticket](../.gitbook/assets/demo-23-changes-mirrored-in-ticket.png)

---

## One Task at a Time, End to End

DuploCloud doesn't hand you a list of recommendations — it works through them. Each phase of the plan is broken into discrete tickets, and the agent executes them one by one: running commands, validating results, and moving to the next. Whether a task is handled autonomously or picked up by a team member via Claude Code, every action is logged and every outcome is verified before the project moves forward.

![Tickets executed one by one](../.gitbook/assets/demo-tackle-tasks.png)
