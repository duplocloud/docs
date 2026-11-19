---
description: Common problems with Kubernetes Upgrader and how to fix them.
---

# Troubleshooting and FAQ

## Common problems

| What you see | What it means | What to do |
| --- | --- | --- |
| **Create plan fails with `PLAN_BLOCKED`** | The plan has a blocker: a downgrade or skipped minor, a target the nodes cannot follow (version skew), a managed node group that would fall out of skew, an add-on without a compatible version, or an EKS upgrade-readiness error. | Read the list of blockers, fix them or change the target, and create the plan again. |
| **`RISKS_NOT_ACCEPTED`** | The plan has risks (missing image, too little EC2 capacity) that you did not accept. | Review the risks and select the accept checkbox, then create the plan. |
| **`PLAN_EXPIRED`** | You did not approve within the approval window (5 minutes by default). Nothing changed. | Create a new plan and approve it in time. |
| **`PLAN_CHANGED`** | The cluster changed while you reviewed. | Review the new plan and approve it. |
| **A second job is refused (409)** | Only one active job is allowed per cluster, even if the cluster is registered twice. | Wait for the active job to finish or cancel it. |
| **"Access denied" on the form, or buttons are disabled** | Your user lacks the permission. | Ask an administrator for the permission (see [Permissions and Safety](permissions-and-safety.md)). |
| **"did not answer within 10 s (private endpoint...)"** | The cluster's Kubernetes API is private-only or not reachable from DuploCloud. | Plans finish with warnings, or block a node swap. Make the API reachable, or skip node swapping. |
| **Job is "Paused, waiting for a valid token"** | The scope's credential expired, was revoked or the portal was unreachable. | Update the credential on the scope. The job resumes within about 30 seconds. |
| **Drain blocked** | A PodDisruptionBudget never allows eviction, or a pod has no controller. The job lists the blocking pods. | Fix the PodDisruptionBudget or move the pod. The job retries by itself. If it ends Failed, run `kubectl uncordon` on the old nodes to go back, or create a new job to finish. |
| **New nodes never became Ready** | New nodes did not join the cluster or the CNI is not ready (about 20 minutes). Old nodes are untouched. | Fix the cause. The job retries from the readiness check. To back out, terminate the new instances and set the group back to the values in its `duplocloud:eks-upgrade:orig-*` tags. |
| **An add-on failed** | The job stopped before the next step. | Repair the add-on in EKS, then create a new job. |
| **Cluster changed after approval** | The job fails before changing anything. | Create a new job. |

<!-- VERIFY: error codes and messages from the extension README; confirm the user-visible wording in QA. -->

## If something was left behind

These are normally cleaned up automatically, within 15 minutes for the guard policy and 5 minutes for cluster-autoscaler. If an upgrade was interrupted:

- **Guard policy on the Duplo-Master role:** remove it with `aws iam delete-role-policy --role-name <role> --policy-name <name from the job result>`.
- **cluster-autoscaler left at 0:** scale it back with `kubectl -n <namespace> scale deploy/<name> --replicas=<n>`. The original count is in the `eks-upgrade.duplocloud.net/original-replicas` annotation. Then remove the two `eks-upgrade.duplocloud.net/*` annotations.

## FAQ

**Can I undo an upgrade?** No. A control-plane upgrade is irreversible, and Cancel does not undo finished steps.

**Can I upgrade more than one minor version at once?** Yes. The plan walks one minor version at a time and adds add-on steps and node swaps as needed.

**Why do I have to approve within 5 minutes?** So you approve a plan that still matches the cluster. Create a new plan if it expires.

**Does it upgrade Karpenter or Fargate nodes?** No. They are listed in the plan and checked for version skew, but not rotated here.

**Can someone else approve my plan?** Yes. Grant `eks-upgrade.approve` to a different person than the one who creates jobs.

**Does Ask AI change my cluster?** Only if you approve a command in the panel.

<!-- VERIFY: FAQ list is a first guess. Bhushan to add the questions customers actually ask. -->
