---
description: Connect DuploCloud to your existing AWS infrastructure and start working immediately.
---

# Connect to Existing Infrastructure

If you already have AWS infrastructure running — VPCs, EKS clusters, RDS databases, workloads — you can connect DuploCloud to it without changing or reprovisioning anything. Once connected, the AI can operate, troubleshoot, and optimize your environment immediately.

## How it works

1. **Add your AWS account as a Provider** — supply credentials and define the scope of access (regions, resource types, accounts). See [Integrating Providers](../../../getting-started/integrating-providers/README.md).
2. **Create a Workspace** — a Workspace is where all work happens. Attach your Provider scope and the relevant skills to it.
3. **Start working** — create a Ticket in the HelpDesk and describe what you want to do. The AI agent operates within the boundaries you defined.

No resource creation, no infrastructure changes, no migration required.

## Examples

<table data-view="cards">
  <thead>
    <tr>
      <th>Title</th>
      <th>Description</th>
      <th data-card-target data-type="content-ref">Target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Cost Optimization</strong></td>
      <td>Identify unused resources, over-provisioned instances, and reserved instance opportunities.</td>
      <td><a href="example-cost-optimization.md">Cost Optimization</a></td>
    </tr>
    <tr>
      <td><strong>Security and Compliance</strong></td>
      <td>Audit AWS against SOC 2 controls, fix GuardDuty gaps, and apply logging changes via Terraform PR.</td>
      <td><a href="example-security-compliance.md">Security and Compliance</a></td>
    </tr>
    <tr>
      <td><strong>AWS Performance Dashboard</strong></td>
      <td>Build a reusable CloudWatch dashboard covering EKS, RDS, EC2, and ALB metrics.</td>
      <td><a href="example-performance-dashboard.md">AWS Performance Dashboard</a></td>
    </tr>
    <tr>
      <td><strong>Developer Self-Service via Slack</strong></td>
      <td>Let developers request S3 buckets, RDS instances, and other AWS resources from Slack — agent provisions and closes the Jira ticket autonomously.</td>
      <td><a href="example-developer-self-service.md">Developer Self-Service via Slack</a></td>
    </tr>
    <tr>
      <td><strong>Infrastructure Audit and Hardening</strong></td>
      <td>Connect an existing EKS workload and bring it to production-ready — observability, security controls, cost guardrails, and CI/CD pipeline.</td>
      <td><a href="example-infrastructure-audit.md">Infrastructure Audit and Hardening</a></td>
    </tr>
    <tr>
      <td><strong>Troubleshooting and Root Cause Analysis</strong></td>
      <td>Investigate EKS pod crashes, RDS slow queries, ALB errors, and unexpected cost spikes using the agent as first responder.</td>
      <td><a href="example-troubleshooting.md">Troubleshooting and Root Cause Analysis</a></td>
    </tr>
  </tbody>
</table>
