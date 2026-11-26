---
description: What Kubernetes Upgrader can read and change, who can use it, and which actions need approval.
---

# Permissions and Safety

## What it can read and change

Kubernetes Upgrader acts with the identity of the scope the cluster was registered with.

| | What it does |
| --- | --- |
| **Reads** | Clusters, add-ons, node groups, Auto Scaling groups, launch templates and AMIs, EC2 quotas and subnets, ECR images, EKS upgrade insights, and the cluster's Kubernetes objects (nodes, pods, workloads, PodDisruptionBudgets, volumes, events). |
| **Changes, only after approval** | The EKS control-plane version, EKS add-on versions, EKS managed node group versions, launch templates (a new default version) and Auto Scaling group size, and the cluster's nodes (cordon, drain, and terminate the old ones). It restarts workloads to move them off old nodes, pauses the cluster autoscaler during a node swap, and attaches a temporary guard policy to the Duplo-Master role. |
| **Never** | Rolls back a finished step, edits a job after its plan is made, terminates a node it didn't cordon and drain, or touches node groups the plan doesn't rotate. |

## Who can use it

Kubernetes Upgrader is for DuploCloud administrators only, because it upgrades clusters with cloud credentials.

| | Read-only user | Regular user | Administrator |
| --- | :---: | :---: | :---: |
| See Kubernetes Upgrader in the menu | No | No | Yes, in **AI Admin** |
| See clusters, jobs and plans | No | No | Yes |
| Register clusters, create, approve, reject, cancel and resume jobs | No | No | Yes |
| Use **Ask AI** and the `kubectl` console | No | No | Yes |

Users without the Administrator role are refused every request, even if a permission set grants them the clusters, the upgrade jobs or the `eks-upgrade.*` actions. The permission editor still lists those actions, but today they don't give access.

Being an administrator doesn't skip the safety checks:

- **Scopes.** You can only use a scope attached to the cluster's workspace. Each use is logged.
- **Approval.** You approve the exact plan, within its approval window, by typing the cluster name. If the cluster changed since the plan was made, you approve the new plan instead.
- **One job per cluster**, and no deleting a cluster while its job runs.

Any administrator can approve a plan, including the one who made it. Kubernetes Upgrader can't require a second person.

The `kubectl` console and Ask AI read the cluster with the scope's identity, which may see every namespace.

## What needs approval

- **Every upgrade.** A job runs only after an administrator approves the exact plan, within its approval window (5 minutes by default), by typing the cluster name. If the cluster changed in the meantime, the new plan has to be approved instead.
- **Risks.** An image that can't be pulled, or too little EC2 capacity, is a risk you must accept when you create the plan and again when you approve. Acceptances are written to the job's audit log.
- **Ask AI commands.** Anything other than plain read-only commands waits for you to approve it in the panel.

## Safety checks

The plan is **blocked**, and no job can be created, when:

- the target is a downgrade, or skips a minor version,
- nodes the job doesn't rotate (standalone, Karpenter or skipped groups) would end up more than three minor versions behind the control plane,
- a managed node group isn't active, or an add-on has no version compatible with the target,
- EKS upgrade insights report an error,
- the Kubernetes API can't be reached and self-managed groups need rotating, or
- the scope's identity lacks a required Kubernetes permission.

While a job runs, rotating worker nodes is the destructive part, so it is guarded:

- **New nodes must be Ready first.** Each group needs as many new Ready nodes as it had old ones before any old node is touched.
- **Only drained nodes are terminated.** Each old node is cordoned and drained, then that exact instance is terminated. The Auto Scaling group never picks what to remove.
- **Drains honour PodDisruptionBudgets.** A budget that never allows eviction, or a drain that times out, stops the swap and lists the blocking pods. Old nodes stay in place.
- **Pods without a controller are not evicted.** They would not be recreated, so they block the drain until you move or delete them.
- **Matching images only.** New nodes must keep the same OS family, CPU architecture and accelerator type. Otherwise the group is skipped, never converted.
- **Add-on health.** A degraded or failed add-on stops the job before the next step.
- **Auto Scaling guard.** During a self-managed swap, a temporary inline policy on the Duplo-Master role stops DuploCloud from changing the cluster's Auto Scaling groups. The job's own session is exempt. The cluster autoscaler is paused and restored. Both are cleaned up automatically if a job is interrupted.
- **Plan integrity.** The job checks that the stored plan matches the approved one, and that the cluster still matches it, before the first step.
- **One job per cluster.** A second active job on the same EKS cluster is refused, even if the cluster is registered twice.

## Limits you should know

- **There is no rollback.** A control-plane upgrade can't be undone. Cancel stops at the next safe point and leaves finished steps applied.
- **Swaps need spare capacity.** A self-managed group temporarily runs twice its nodes during the swap; EKS managed node groups add a smaller surge. Check EC2 quotas and free IP addresses. The pre-flight check warns you.
- **Strict PodDisruptionBudgets** (for example `maxUnavailable: 0`) block the drain.
- **Launch template versions stay.** The new default launch template version created for a swap is kept, even if the job is cancelled.

## AI data handling (Ask AI)

- **What is sent:** the job's state and plan as text (cluster name, region, versions, steps, node, workload and image names, pre-flight results, and the recent audit log, which contains the email addresses of the people who approved or cancelled) and your questions. It goes to the AI agent configured for the workspace. Kubernetes Upgrader doesn't call a model itself.
- **Where it is kept:** each conversation is a platform ticket, stored like any HelpDesk ticket. **New chat** closes it.
- **Credentials:** the cluster's scope is attached to the session so the agent can run `kubectl` and `aws` commands, and the agent acts with your DuploCloud session. Credentials are never put in the message text.
- **Guardrails:** without your approval, the agent can only run read-only commands: `kubectl get`, `describe`, `logs`, `top`, `events`, `explain`, `version` and similar (never on secrets), `aws` `describe-`, `list-` and `get-` calls (nothing that reads secrets, parameters or credentials), and reads of this job and cluster. Everything else waits for **Approve & run**.
