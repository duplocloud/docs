---
description: Upgrade Kubernetes clusters with a plan you approve first.
icon: robot
---

# Kubernetes Upgrader

Upgrade your Amazon EKS clusters as one tracked job, with a plan you approve first. Kubernetes Upgrader upgrades the control plane, the managed add-ons and the worker nodes in the order AWS recommends, shows live progress, and stops safely when something looks wrong.

{% hint style="warning" %}
Kubernetes Upgrader can change your cluster and terminate worker nodes. It is available to administrators. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

<!-- VERIFY: admin-only is the decision from Zafar and Bhushan on 2026-11-19 (ClickUp DUPLOAI-5602). Confirm the final wording once the menu move ships. -->

## What it does

An upgrade job can run up to three phases, always in this order:

1. **Control plane**: upgrades the EKS control plane to the version you choose. EKS moves one minor version at a time, so a multi-version upgrade is planned as a series of steps.
2. **Add-ons**: upgrades the EKS add-ons (such as `vpc-cni`, `coredns`, `kube-proxy` and `aws-ebs-csi-driver`) to versions that match the new control plane, keeping their existing configuration and IAM roles.
3. **Worker nodes**: replaces worker nodes with nodes on the new Kubernetes version. Self-managed Auto Scaling groups are rotated with new nodes first, then old nodes are cordoned, drained and terminated. EKS managed node groups are upgraded with EKS's own rolling update.

You choose which phases to run. Every job follows **plan, approve, run**: creating a job only builds the plan and runs pre-flight checks. Nothing changes in your cluster until someone with permission approves that exact plan.

## Who it is for

Platform and DevOps administrators who run EKS clusters and want a repeatable, reviewed upgrade instead of a manual runbook.

## What it works with

| | |
| --- | --- |
| Clouds | AWS (commercial regions and AWS GovCloud (US)) |
| Clusters | Amazon EKS, standard and extended support versions that EKS offers |
| Worker nodes | Self-managed Auto Scaling groups (Amazon Linux 2, Amazon Linux 2023, Ubuntu EKS; x86_64 and arm64) and EKS managed node groups |
| Not rotated | Karpenter and EKS Auto Mode nodes, Fargate, standalone EC2 nodes, Bottlerocket and Windows self-managed groups (the plan lists them and checks version skew) |

<!-- VERIFY: free or paid. The Release 1 listing and console decide this; the repo does not say. -->

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need before you start, how to activate Kubernetes Upgrader from the Agent Marketplace, and how to connect it to your accounts. |
| [Use](use.md) | Step-by-step walkthroughs of the main things Kubernetes Upgrader does. |
| [Permissions and Safety](permissions-and-safety.md) | What Kubernetes Upgrader can read and change, which actions need approval, and how it behaves for read-only, regular and admin users. |
| [Troubleshooting and FAQ](troubleshooting.md) | Common problems with Kubernetes Upgrader and how to fix them. |
