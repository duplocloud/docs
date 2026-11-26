---
description: What Kubernetes Upgrader can read and change, which actions need approval, and who can use it (administrators only).
---

# Permissions and Safety

## What it can read and change

Kubernetes Upgrader acts with the IAM identity of the AWS scope you registered the cluster with.

| | What it does |
| --- | --- |
| **Reads** | Clusters, add-ons, node groups, Auto Scaling groups, launch templates and AMIs, EC2 quotas and subnets, ECR images, and the cluster's Kubernetes objects (nodes, pods, workloads, PodDisruptionBudgets, volumes, events). |
| **Changes (only after approval)** | The EKS control-plane version, EKS add-on versions, EKS managed node group versions, launch templates and Auto Scaling group capacity, and the cluster's nodes (cordon, drain, terminate old nodes). It also restarts workloads to move them, and pauses cluster-autoscaler during a node swap. |
| **Never** | It does not roll back a finished step, edit a job after the plan is made, or touch groups created after you approved the plan. |

## Who can use it

Kubernetes Upgrader is **administrator-only**. It is in **AI Admin > Kubernetes Upgrader**, and people without the Administrator role are refused, whatever their permission sets say: they see no menu entry, and every request to its API is refused (`ADMIN_ONLY`). That covers the cluster and job pages, the `kubectl` console and **Ask AI**.

| User | What they can do |
| --- | --- |
| **Administrator** | Everything: register clusters, create and approve upgrade jobs, cancel and resume them, use the `kubectl` console and Ask AI. Each use of a scope through the Administrator role is recorded in the audit log. |
| **Anyone else** (read-only or regular, whatever their permission sets grant) | Nothing. There is no menu entry, and every request is refused. |

Being an administrator opens Kubernetes Upgrader. It doesn't skip any of the checks on this page: every upgrade still needs an approved plan, and every safety check still applies.

The platform's named actions (`eks-upgrade.approve`, `eks-upgrade.kubectl` and `eks-upgrade.discover`) are still declared, but only administrators reach them, so there is nothing to grant.

An administrator can use any AWS scope attached to the cluster's workspace. A scope from another workspace is always refused, and the message says why.

## What needs approval

- **Every upgrade.** A job runs only after an administrator approves the exact plan within **5 minutes** and types the cluster name. An approval without the cluster name is refused. A plan that changes before approval has to be reviewed again.
- **Risks.** An unavailable image or too little EC2 capacity is a risk you must accept in the form, and again when you approve. Acceptances are written to the audit log.
- **Ask AI.** Anything other than plain read-only commands needs your approval in the panel.

## Safety checks

Rotating worker nodes is the destructive part, so it is guarded:

- **Only what was cordoned and drained is terminated.** Each instance is terminated explicitly. The Auto Scaling group never chooses what to remove.
- **New nodes must be Ready** before old nodes are touched. If the check fails, nothing is touched.
- **Drain must finish** before old nodes are terminated. A PodDisruptionBudget that never allows eviction, or a drain that times out (30 minutes by default), keeps the old nodes and lists the blocking pods.
- **Add-on health gate.** A degraded or failed add-on stops the job before the next step.
- **Auto Scaling guard.** During a node swap, an inline policy that denies `autoscaling:*` on the cluster's groups is attached to the Duplo-Master role, then always removed when the job ends. Only the job's own session is exempt, so the job can still act when it reaches AWS through a DuploCloud scope. cluster-autoscaler is paused and restored.
- **Plan integrity.** The job re-checks that the stored plan matches the approved plan and that the cluster still matches before the first step.
- **Image and OS checks.** New nodes must match the Kubernetes version, OS family, CPU architecture and accelerator type. Otherwise the group is skipped, never converted.
- **One active job per cluster.** A second job on the same cluster is refused.
- **Scope check on every read.** Every request that reads the cluster with its scope checks that the scope belongs to the cluster's workspace, not only creating and approving a job.
- **Input checks.** The region, cluster name and add-on names must be real AWS and EKS values.
- **Safe to disable mid-job.** If Kubernetes Upgrader is disabled while a job runs, the job pauses at a safe point, removes the guard policy and drops its cached credentials. When it's enabled again, the job continues where it stopped, without swapping nodes twice.

## Limits you should know

- There is **no rollback**. A control-plane upgrade is irreversible. Cancel stops at the next safe point and does not undo finished steps.
- A node swap temporarily doubles the capacity of each rotated group. Check quotas and free IP addresses.
- Strict PodDisruptionBudgets (for example `maxUnavailable: 0`) block the drain.
- Bare pods are evicted like any pod. One whose image risk you accepted is deleted and not recreated.

## AI data handling (Ask AI)

- **What is sent:** the job's state and plan as text (cluster name, region, versions, steps, node, workload and image names, pre-flight results, and the recent audit log, which contains approvers' email addresses) plus your questions. It goes to the AI agent configured for the workspace. Kubernetes Upgrader does not call a model itself.
- **Where it is kept:** each job's conversation is a platform ticket, stored like any HelpDesk ticket. **New chat** closes it.
- **Credentials:** the cluster scope is attached to the session so the agent can run `kubectl` and `aws` commands. Your session token is passed in the request context, never in the message text.
- **Who can open it:** administrators only, like the rest of Kubernetes Upgrader.
- **Guardrails:** commands that change the cluster or AWS need your approval. Without approval only plain read-only commands run: `kubectl get`, `describe`, `logs`, `top` and `events` (never secrets), and `aws ... describe-`, `list-` and `get-` calls (nothing secret or credential related).

