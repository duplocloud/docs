---
description: Connect an existing AWS service to DuploCloud and get it from zero observability to production-ready — with security hardening, cost controls, and automated pipelines.
---

# Example: Infrastructure Audit and Hardening

This example shows how to connect an existing AWS workload to DuploCloud and systematically bring it up to production standards — adding observability, applying security controls, setting cost guardrails, and establishing automated deployment pipelines.

For the end-to-end generic walkthrough, see [How to Manage Large Complex Projects](../../../../common-use-cases/how-to-manage-large-complex-projects.md).

## Prerequisites

* DuploCloud is installed and running.
* An AWS Provider with read/write access to your account is connected.
* (Optional) A Kubernetes Provider is connected if your workload runs on EKS.

## The scenario

An order service running on AWS EKS has no observability, no cost controls, no automated deployment pipeline, and no security hardening. The goal: connect it to DuploCloud and get it production-ready.

{% stepper %}
{% step %}
## Connect your AWS and Kubernetes providers

Navigate to **AI Admin → Providers** and verify:

* Your **AWS Provider** is connected with credentials and scope covering the account and regions where your workload runs.
* Your **Kubernetes Provider** is connected with scope covering the namespaces your service uses.

Confirm the connection is live by asking the agent to list running nodes and pods in the Workspace.
{% endstep %}

{% step %}
## Create a Project and define requirements

Navigate to **AI DevOps → Projects** and create a new Project. Open the **AI Planner** and provide a prompt describing your workload and goals:

> "We have an order service running on AWS EKS. It has 5-10 microservices, no observability, no cost controls, no deployment pipeline, and no security hardening. We need to pass a SOC 2 audit in 90 days. Create a plan covering: observability setup, security hardening, cost controls, and CI/CD pipeline."

The planner generates a structured spec with all tasks prioritised and sequenced.
{% endstep %}

{% step %}
## Set up observability

With the plan approved, instruct the agent to set up observability:

> "Set up CloudWatch dashboards for our EKS pods and nodes. Configure log groups for all services and set up alarms for CPU > 80% and memory > 85%."

The agent creates CloudWatch log groups, metric filters, alarms, and a dashboard covering your key health indicators.
{% endstep %}

{% step %}
## Security hardening

Ask the agent to identify and resolve security gaps:

> "Audit the security posture of our AWS account. Check for open security groups, public S3 buckets, missing encryption, and any IAM policies with excessive permissions."

The agent scans your account and returns a prioritised list of findings. You can instruct it to remediate each category:

* Tighten security group rules
* Enable S3 server-side encryption and block public access
* Scope down over-permissive IAM roles
* Enable AWS Config and CloudTrail where missing

{% hint style="warning" %}
Security group changes can affect live traffic. Review the planned changes carefully and apply during a low-traffic window.
{% endhint %}
{% endstep %}

{% step %}
## Cost controls

Ask the agent to identify cost optimisation opportunities:

> "Analyse our EC2 and RDS instances for right-sizing opportunities. Identify idle resources and over-provisioned reserved instances."

The agent returns a breakdown of potential savings by resource type and recommends specific instance size changes or terminations.
{% endstep %}

{% step %}
## CI/CD pipeline

Ask the agent to set up or review your deployment pipeline:

> "Review our EKS deployment setup and recommend improvements for automated rollouts with rollback support."
{% endstep %}
{% endstepper %}

## What a typical audit covers

| Area | What the agent checks |
|---|---|
| EKS | Node utilization, pod restarts, namespace RBAC, network policies |
| EC2 | Instance sizing, idle instances, missing tags |
| RDS | Multi-AZ status, backup retention, encryption at rest |
| S3 | Public access, encryption, lifecycle policies, versioning |
| IAM | Wildcard policies, unused roles, root account MFA |
| Networking | Open security groups, public subnets with sensitive resources |
| CloudTrail | Logging enabled in all regions, log file validation |
