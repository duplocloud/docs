---
description: What Kubernetes Upgrader can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

## What it can read and change

Kubernetes Upgrader acts with the IAM identity of the AWS scope you registered the cluster with.

| | What it does |
| --- | --- |
| **Reads** | Clusters, add-ons, node groups, Auto Scaling groups, launch templates and AMIs, EC2 quotas and subnets, ECR images, and the cluster's Kubernetes objects (nodes, pods, workloads, PodDisruptionBudgets, volumes, events). |
| **Changes (only after approval)** | The EKS control-plane version, EKS add-on versions, EKS managed node group versions, launch templates and Auto Scaling group capacity, and the cluster's nodes (cordon, drain, terminate old nodes). It also restarts workloads to move them, and pauses cluster-autoscaler during a node swap. |
| **Never** | It does not roll back a finished step, edit a job after the plan is made, or touch groups created after you approved the plan. |

## Who can do what

Access follows the DuploCloud platform permission model. The cluster and job pages sit under your workspace. Three actions are granted separately, and the "all" permission does not include them.

| Action | Permission | What it allows |
| --- | --- | --- |
| Approve, reject, cancel, resume a job | `eks-upgrade.approve` (marked destructive) | Starts the control-plane upgrade and node termination. Grant it separately from creating a job, so a different person can approve. |
| Use the `kubectl` console | `eks-upgrade.kubectl` | Reads the cluster with the scope's identity, which may see every namespace. |
| Discover clusters | `eks-upgrade.discover` | Lists the clusters an AWS scope can see. |

| User | What they can do |
| --- | --- |
| **Read-only** | View clusters and jobs. Cannot add or delete a cluster, create a job, approve, reject, cancel, resume or use `kubectl`. The buttons are disabled with a message. |
| **Regular user** | Whatever their permission sets grant in the workspace: for example create a job, but not approve it. |
| **Administrator** | Everything, including approving upgrades. Each use through the administrator role is recorded in the audit log. |

<!-- VERIFY: read-only and regular rows are derived from Permissions.cs and the README access-control table. Confirm against QA with a read-only and a regular test user (screenshots KU-12 to KU-14). -->
<!-- VERIFY: Zafar and Bhushan decided on 2026-11-19 that Kubernetes Upgrader is admin-only and moves from the DevOps menu to the Admin menu (DUPLOAI-5602). Rewrite this table to match the shipped behaviour. -->

A user can only use scopes their permission sets allow in the workspace. Administrators can use any scope attached to the workspace. A scope from another workspace is always refused, and the message says why.

## What needs approval

- **Every upgrade.** A job runs only after someone with `eks-upgrade.approve` approves the exact plan within **5 minutes** and types the cluster name. A plan that changes before approval has to be reviewed again.
- **Risks.** An unavailable image or too little EC2 capacity is a risk you must accept in the form, and again when you approve. Acceptances are written to the audit log.
- **Ask AI.** Anything other than plain read-only commands needs your approval in the panel.

## Safety checks

Rotating worker nodes is the destructive part, so it is guarded:

- **Only what was cordoned and drained is terminated.** Each instance is terminated explicitly. The Auto Scaling group never chooses what to remove.
- **New nodes must be Ready** before old nodes are touched. If the check fails, nothing is touched.
- **Drain must finish** before old nodes are terminated. A PodDisruptionBudget that never allows eviction, or a drain that times out (30 minutes by default), keeps the old nodes and lists the blocking pods.
- **Add-on health gate.** A degraded or failed add-on stops the job before the next step.
- **Auto Scaling guard.** During a node swap, an inline policy that denies `autoscaling:*` on the cluster's groups is attached to the Duplo-Master role, then always removed when the job ends. cluster-autoscaler is paused and restored.
- **Plan integrity.** The job re-checks that the stored plan matches the approved plan and that the cluster still matches before the first step.
- **Image and OS checks.** New nodes must match the Kubernetes version, OS family, CPU architecture and accelerator type. Otherwise the group is skipped, never converted.
- **One active job per cluster.** A second job on the same cluster is refused.

## Limits you should know

- There is **no rollback**. A control-plane upgrade is irreversible. Cancel stops at the next safe point and does not undo finished steps.
- A node swap temporarily doubles the capacity of each rotated group. Check quotas and free IP addresses.
- Strict PodDisruptionBudgets (for example `maxUnavailable: 0`) block the drain.
- Bare pods are evicted like any pod. One whose image risk you accepted is deleted and not recreated.

## AI data handling (Ask AI)

- **What is sent:** the job's state and plan as text (cluster name, region, versions, steps, node, workload and image names, pre-flight results, and the recent audit log, which contains approvers' email addresses) plus your questions. It goes to the AI agent configured for the workspace. Kubernetes Upgrader does not call a model itself.
- **Where it is kept:** each job's conversation is a platform ticket, stored like any HelpDesk ticket. **New chat** closes it.
- **Credentials:** the cluster scope is attached to the session so the agent can run `kubectl` and `aws` commands. Your session token is passed in the request context, never in the message text.
- **Guardrails:** commands that change the cluster or AWS need your approval. Without approval only plain read-only commands run: `kubectl get`, `describe`, `logs`, `top` and `events` (never secrets), and `aws ... describe-`, `list-` and `get-` calls (nothing secret or credential related).

<!-- VERIFY: all text above comes from the extension README (Safety model, Known limitations, AI data handling). Bhushan to confirm it matches the shipped version (0.9.15 or later). -->
