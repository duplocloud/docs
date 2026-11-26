---
description: Common problems with Kubernetes Upgrader and how to fix them.
---

# Troubleshooting and FAQ

## Common problems

| What you see | What it means | What to do |
| --- | --- | --- |
| **The upgrade is blocked** (`PLAN_BLOCKED`) | The plan has a blocker (see [Safety checks](permissions-and-safety.md#safety-checks)), such as a skipped minor version, nodes that would fall too far behind, an inactive managed node group, an add-on without a compatible version, or an EKS upgrade-insight error. | Read the blockers, fix them or change the target, and create the plan again. |
| `RISKS_NOT_ACCEPTED` | The plan has risks, such as a missing image or too little EC2 capacity, that weren't accepted. | Review the risks, tick the accept box, and try again. |
| `PLAN_EXPIRED`: "The plan was not approved within its approval window…" | Nobody approved within the approval window (5 minutes by default). Nothing changed. | Create a new job and approve it in time. |
| `PLAN_CHANGED` | The cluster changed while the plan waited. | Review the new plan and approve it. |
| "Upgrade job '…' is still running on this cluster" (or "still waiting for approval"). "Finish, reject or delete it first." | Only one active job is allowed per EKS cluster, even if it's registered twice. | Wait for that job to finish, or reject or cancel it. |
| "Upgrade jobs cannot be edited after they are planned — create a new job instead." | A job's plan is fixed once made. | Create a new job. |
| **Kubernetes Upgrader isn't in the menu**, or "The Kubernetes Upgrader is available to platform Administrators only. It is in the AI Admin menu." | Only administrators can use it, and it's in the **AI Admin** menu. | Sign in as an administrator, or ask one to run the upgrade (see [Permissions and Safety](permissions-and-safety.md#who-can-use-it)). |
| **No clusters are listed** | The **Workspace** list at the top of **Kubernetes Clusters** shows a different workspace. | Choose the workspace the cluster was registered in. |
| "You are not allowed to use this cluster's scope. (Administrator check: the scope is not attached to this workspace)" | The scope the cluster was registered with is no longer attached to the cluster's workspace. | Attach the scope to the workspace again. |
| "Reading the cluster's … timed out — try again." | AWS or the cluster's API was slow to answer. | Try again. If it keeps happening, check that DuploCloud can reach the cluster. |
| "…access denied by AWS for `<action>` — grant it to the scope's IAM identity" | The scope's IAM identity lacks that AWS action. | Add the named action (see [AWS permissions](set-up.md#aws-permissions)) and resume the job or create the plan again. |
| "the cluster rejected the scope's IAM identity (401)" | The identity isn't mapped in the cluster. | Add an EKS access entry (or `aws-auth` mapping) for it. |
| "the cluster's RBAC denied the request (403)" | The identity is mapped but lacks a Kubernetes permission. | Grant the [Kubernetes permissions](set-up.md#kubernetes-permissions). |
| "The cluster's Kubernetes API did not answer within 10 s (private endpoint, or no network path from DuploCloud?)." | The API is private-only or unreachable from DuploCloud. | Make the API reachable from DuploCloud, or skip the self-managed node swap. |
| **Paused — waiting for a valid token** | The scope's credential expired or was revoked. | Update the credential on the scope's provider. The job carries on within about 30 seconds. |
| **Drain blocked** | A PodDisruptionBudget never allows eviction, or a pod isn't managed by a controller. The job lists the blocking pods. | Fix the budget, or move or delete the pod, then select **Resume** if the job failed. |
| **New nodes never became Ready** | New nodes didn't join the cluster, or the CNI wasn't ready, within about 20 minutes. Old nodes are untouched. | Fix the cause and select **Resume**. |
| **An add-on failed** | The job stopped before the next step. | Fix the add-on in EKS, then select **Resume**. |
| **The cluster changed after approval** | The job stopped before changing anything. | Create a new job. |

## If something is left behind

These are cleaned up automatically after an interrupted job: the guard policy within 15 minutes and the cluster autoscaler within 5 minutes. If a job failed part way through a node swap, you may also find:

- **Cordoned old nodes.** Run `kubectl uncordon <node>` to put them back in service, or resume the job to finish the swap.
- **A scaled-out Auto Scaling group.** Its original size is in the group's `duplocloud:eks-upgrade:orig-desired` and `duplocloud:eks-upgrade:orig-max` tags. Resume the job, or set the group back to those values.
- **The guard policy on the Duplo-Master role** (`DuploEksUpgrade-<cluster>-<region>`), if the cleanup couldn't run: remove it with `aws iam delete-role-policy --role-name <role> --policy-name <name>`.
- **The cluster autoscaler left at 0 replicas:** scale it back with `kubectl -n <namespace> scale deploy/<name> --replicas=<n>`. The original count is in its `eks-upgrade.duplocloud.net/original-replicas` annotation. Then remove the two `eks-upgrade.duplocloud.net/*` annotations.

## FAQ

**Can I undo an upgrade?** No. A control-plane upgrade can't be undone, and Cancel doesn't undo finished steps.

**Can I upgrade more than one minor version at once?** Yes. The plan moves one minor version at a time and adds the add-on steps and node swaps needed in between.

**Why must I approve within 5 minutes?** So the plan you approve still matches the cluster. If it expires, create a new job. The platform administrator can change the window.

**Does it upgrade Karpenter, Auto Mode or Fargate nodes?** No. They're listed in the plan and checked for version skew, but not rotated.

**How long does an upgrade take?** It depends on the number of steps and nodes. Each control-plane step is an EKS update, and each node swap waits for new nodes and drains.

**Can someone else approve my plan?** Yes. Any administrator can. Kubernetes Upgrader can't require a second person to approve.

**Can non-administrators use it?** No. Permission sets don't give access; only the Administrator role does.

**Does Ask AI change my cluster?** Only if you approve a command in the panel.

**What happens if I delete a cluster registration?** Its job records are deleted. Nothing changes in AWS or in the cluster. A cluster with a running job can't be deleted.
