---
description: Plans and runs Kubernetes cluster upgrades.
---

# Kubernetes Upgrader

Upgrade your Amazon EKS clusters as one tracked job, with a plan you approve first. Kubernetes Upgrader upgrades the control plane, the managed add-ons and the worker nodes in the order AWS recommends, shows live progress, and stops safely when something looks wrong.

These pages describe Kubernetes Upgrader version 0.9.22.

{% hint style="warning" %}
Kubernetes Upgrader can change your cluster and terminate worker nodes, so it is **administrator-only**. It is in the **AI Admin** menu, and people without the Administrator role can't see or use it, whatever their permission sets say. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

## What it does

An upgrade job can run up to three phases, always in this order:

1. **Control plane**: upgrades the EKS control plane to the version you choose. EKS moves one minor version at a time, so a multi-version upgrade is planned as a series of steps.
2. **Add-ons**: upgrades the EKS add-ons (such as `vpc-cni`, `coredns`, `kube-proxy` and `aws-ebs-csi-driver`) to versions that match the new control plane, keeping their existing configuration and IAM roles.
3. **Worker nodes**: replaces worker nodes with nodes on the new Kubernetes version. Self-managed Auto Scaling groups are rotated with new nodes first, then old nodes are cordoned, drained and terminated. EKS managed node groups are upgraded with EKS's own rolling update.

You choose which phases to run. Every job follows **plan, approve, run**: creating a job only builds the plan and runs pre-flight checks. Nothing changes in your cluster until an administrator approves that exact plan.

## Who it is for

DuploCloud administrators who run EKS clusters and want a repeatable, reviewed upgrade instead of a manual runbook.

## Where to find it

| Where | What's there | Who uses it |
| --- | --- | --- |
| **AI Admin > Kubernetes Upgrader > Kubernetes Clusters** | The registered clusters of the workspace you choose in **Workspace** at the top of the list, their upgrade jobs, live progress, the read-only `kubectl` console and **Ask AI** | DuploCloud administrators |

There is no Kubernetes Upgrader entry in a workspace's menu. Clusters are still registered per workspace and use that workspace's AWS scopes; AI Admin has no workspace selector of its own, so the cluster list has one.

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
| [Set Up](set-up.md) | What you need before you start, how to activate Kubernetes Upgrader from the Agent Marketplace, and how to register your first cluster. |
| [Use](use.md) | Step-by-step walkthroughs of the main things Kubernetes Upgrader does. |
| [Permissions and Safety](permissions-and-safety.md) | What Kubernetes Upgrader can read and change, which actions need approval, and who can use it (administrators only). |
| [Troubleshooting and FAQ](troubleshooting.md) | Common problems with Kubernetes Upgrader and how to fix them. |
