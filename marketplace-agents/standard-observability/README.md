---
description: Set up monitoring for your Kubernetes cluster on AWS.
icon: robot
---

# Standard Observability

Set up logs, metrics and dashboards for an Amazon EKS cluster from one wizard. Standard Observability deploys Loki for logs, Prometheus for metrics and Grafana for dashboards, with sign-in through your DuploCloud portal, and shows its progress phase by phase.

{% hint style="warning" %}
Standard Observability creates and changes AWS and Kubernetes resources in your account: a node pool, an S3 bucket, an S3 VPC endpoint, security group rules, load balancers, and in standalone mode IAM roles. Read [Permissions and Safety](permissions-and-safety.md) before you use it.
{% endhint %}

<!-- VERIFY: who can use it. ClickUp 17twvjx4bm3 is where Pankaj Akhade and Srikar Naramsetty decide admin-only versus user access. The extension code has no permission checks of its own (see Permissions and Safety), so the final wording depends on that decision and on the platform's default permissions for this resource type. -->

## What it does

One stack runs in one namespace of one cluster (default namespace `observability`). Provisioning goes through these parts:

1. **Observability node pool**: one shared EKS node group named `observability-nodepool` (default 2 to 3 `t3.large` nodes) that runs Loki, Grafana, the log collectors and Prometheus. You can instead point the stack at existing nodes by label.
2. **Node networking**: checks the security group rules the pool needs and adds the missing ones.
3. **Log storage**: one S3 bucket for Loki (created for you, or one you provide), plus an S3 gateway VPC endpoint so log traffic to S3 does not go through the NAT gateway.
4. **Loki, Grafana and log collectors**: installed as Flux Helm releases. Collectors send pod logs and cluster events to Loki. Grafana signs users in through your DuploCloud portal.
5. **Prometheus (optional "Monitoring" step)**: Prometheus, node-exporter, kube-state-metrics and the default Kubernetes rules and dashboards. No Alertmanager is installed, so nothing is routed or notified.
6. **Endpoints**: a public load balancer for Grafana, and optional internal load balancers for Loki (log shipping) and Prometheus (remote write) so other clusters can send data in.
7. **Dashboards page**: opens Grafana inside DuploCloud with a dashboard picker you can curate with favourites.

Provisioning is repeatable: each step finds or creates its resource, so after a failure you fix the cause and run it again.

<!-- VERIFY: "run it again" means saving the stack from Edit (the backend re-runs provisioning on a spec change). Confirm there is a supported "re-run" action with no changes. -->

## Who it is for

Platform and DevOps teams who want one standard logging and metrics stack on an EKS cluster instead of building Loki, Prometheus and Grafana by hand for each environment.

## What it works with

| | |
| --- | --- |
| Clouds | AWS |
| Clusters | Amazon EKS |
| Provisioning modes | **DevOps extension mode** (uses the DevOps extension's Environment and Resource Group) and **Standalone mode** (uses only an AWS scope and a Kubernetes scope) |
| Required on the cluster | FluxCD, and the AWS Load Balancer Controller (the wizard marks both as required) |
| Optional on the cluster | cluster autoscaler, external-dns (needed only if you want DNS records created for you) |
| Not supported | Other clouds. The wizard says "AWS only for now". |

<!-- VERIFY: the wizard marks FluxCD and the AWS Load Balancer Controller as required, but the extension README and the run only warn for the Load Balancer Controller (only FluxCD fails a standalone run). Confirm which is true. -->
<!-- VERIFY: free or paid. The repo does not say. The stack creates AWS resources that AWS bills you for (nodes, EBS volumes, S3, load balancers). -->

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need before you start, how to activate Standard Observability from the Agent Marketplace, and how to connect it to your accounts. |
| [Use](use.md) | Step-by-step walkthroughs of the main things Standard Observability does. |
| [Permissions and Safety](permissions-and-safety.md) | What Standard Observability can read and change, which actions need approval, and how it behaves for read-only, regular and admin users. |
| [Troubleshooting and FAQ](troubleshooting.md) | Common problems with Standard Observability and how to fix them. |
