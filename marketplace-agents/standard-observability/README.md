---
description: Set up monitoring for your Kubernetes cluster on AWS.
icon: robot
---

# Standard Observability

Set up logs, metrics and dashboards for an Amazon EKS cluster from one wizard. Standard Observability deploys Loki for logs, Prometheus for metrics and Grafana for dashboards. Grafana signs people in through your DuploCloud portal, and you can open its dashboards without leaving DuploCloud.

{% hint style="warning" %}
Standard Observability creates real AWS and Kubernetes resources in your account: an EKS node group, an S3 bucket, an S3 VPC endpoint, security group rules, IAM roles and load balancers. Read [Permissions and Safety](permissions-and-safety.md) before you create a stack.
{% endhint %}

{% hint style="info" %}
These pages describe Standard Observability **0.1.138**. Some of what they describe (the Administrator setup page, the CloudFormation role template, keeping the Grafana admin password only in the cluster, and the automatic Grafana registration) is new in recent versions. If your Agent Marketplace shows an older version, those parts may be missing.
{% endhint %}

## What it does

One **stack** is one observability setup in one namespace of one EKS cluster. Creating a stack:

1. **Adds an observability node pool.** One shared EKS node group, `observability-nodepool` (2 to 3 `t3.large` nodes by default), runs Loki, Grafana and Prometheus. You can use existing nodes instead.
2. **Stores logs in S3.** Loki keeps logs in one S3 bucket, for one year by default. An S3 gateway VPC endpoint keeps that traffic off your NAT gateway.
3. **Collects logs.** Grafana Alloy sends every pod's logs and the cluster's events to Loki.
4. **Collects metrics (optional).** Prometheus with node-exporter, kube-state-metrics and the default Kubernetes dashboards and rules. No Alertmanager is installed, so alerts are not sent anywhere.
5. **Publishes Grafana.** Grafana sits behind a public load balancer with your certificate and hostname, and signs people in through your DuploCloud portal. Optional internal load balancers let other clusters send logs and metrics in.
6. **Shows the dashboards in DuploCloud.** The **Standard Observability** page opens Grafana inside DuploCloud, with a dashboard picker you can tailor.

The stack page shows each phase as it runs, every resource the stack created, and what it removes and keeps when you tear it down.

## Who it is for

Platform and DevOps teams who want one standard logging and metrics stack for an EKS cluster, instead of building Loki, Prometheus and Grafana by hand.

## Where to find it

Under **Observability > Standard Observability** in the left menu. Where it takes you depends on the workspace:

| Workspace has | You land on |
| --- | --- |
| No stack | A page with a button to create one |
| A finished stack | The dashboards page |
| Only stacks still being built | The newest stack's page |

From the dashboards page, the gear icon opens the stack's page. **All Stacks** on the stack page lists every stack in the workspace.

Administrators also have a setup page, under **Agent Setup > Standard Observability** in the Administrator area. See [Set Up](set-up.md).

## What it works with

| | |
| --- | --- |
| Cloud | AWS only |
| Cluster | Amazon EKS, with **FluxCD** and the **AWS Load Balancer Controller** running |
| Optional on the cluster | Cluster autoscaler, so the node pool can scale. external-dns, if you want DNS records created for you. |
| Credentials | An **AWS scope** and a **Kubernetes scope** for the cluster, both attached to the workspace. One IAM role can serve both. |
| Modes | **Standalone**: uses only the AWS and Kubernetes scopes. **Use the DevOps extension**: also uses the workspace's DevOps environment and resource group, and is offered only where that extension is available. |
| Not covered | Other clouds, Alertmanager and alert routing, installing cluster add-ons, and collector-only setups for other clusters |

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need, the IAM role and Kubernetes access, activating the agent and choosing default scopes. |
| [Use](use.md) | Create a stack, follow it, create the DNS record, open dashboards, tailor favourites, edit and tear down. |
| [Permissions and Safety](permissions-and-safety.md) | What it reads and changes, who can do what, what needs confirmation, and how it protects existing resources. |
| [Troubleshooting and FAQ](troubleshooting.md) | Messages you might see and how to fix them. |

The platform's own **Standard Observability Suite**, which is a different feature, is described under [Diagnostics](../../automation-platform/diagnostics-overview/standard-observability-suite/README.md).
