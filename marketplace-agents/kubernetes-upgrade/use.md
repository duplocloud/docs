---
description: Step-by-step walkthroughs of the main things Kubernetes Upgrader does.
---

# Use

## Upgrade a cluster

1. Open **Kubernetes Upgrader > Kubernetes Clusters** and select a cluster.
2. Select **Add Job** (Add Upgrade Job).
3. Choose what to upgrade. Select at least one:
   - **Control Plane Upgrade**: pick the target version. Every version EKS offers above the current one is listed with its support status. Multi-version targets are planned as one step per minor version.
   - **Add-on Upgrade**: for each add-on, the current and target versions are shown. The target is previewed against the version you selected.
   - **Worker Node Swap**: lists every self-managed Auto Scaling group and EKS managed node group, with capacity and Kubernetes version.
4. Check the **Upgrade Path** section. It previews every step, including add-on steps after each control-plane step and any extra node swap needed to stay inside the Kubernetes version-skew limit.
5. If you are swapping nodes, select **Run pre-flight checks**. **Create plan** stays disabled until the checks have run.
6. Review any risks the checks found, such as images that cannot be pulled or not enough EC2 capacity. To continue, accept the risk with the checkbox.
7. Select **Create plan**. Nothing has changed in your cluster yet.

If the plan is blocked (for example, the target is too far ahead of the nodes), the form shows why and **Upgrade** stays disabled.

<!-- VERIFY: button and section names on the Add Job form (screenshots KU-05 to KU-07). -->

## Review and approve the plan

1. On the job page, review the plan: the upgrade path, add-ons, worker groups, pre-flight results, images, EC2 capacity and workload availability.
2. Select **Approve** and type the cluster name to confirm, or select **Reject**.

You have **5 minutes** to approve a plan. After that the job expires and nothing is changed. If the cluster changed while you reviewed, you are asked to review a fresh plan.

Only approved jobs run. If something changed in the cluster after approval, the job fails before it changes anything and you create a new job.

<!-- VERIFY: approval window default (5 min) is configurable by the platform admin. Screenshots KU-08, KU-09. -->

## Follow progress

The job page refreshes about every 5 seconds until the job finishes. It shows:

- a banner with the current state,
- an **Upgrade Path** stepper with each step's status and duration,
- a card per phase ("step i of n", "round r of R"),
- a live node table,
- a read-only `kubectl` console, for users who have the permission.

A full upgrade usually takes 15 to 40 minutes. Multi-version upgrades take longer.

## Cancel a running upgrade

Select **Cancel upgrade** on the job page. The job stops at the next safe point. Nothing is rolled back and finished steps stay applied. A control-plane or add-on update that EKS is already running cannot be stopped, so the job stops after it finishes. If hosts are already being swapped, the swap finishes first.

## Resume after a pause

If your cloud credentials expire during a run, the job pauses with "waiting for a valid token" and checks again every 30 seconds. Update the scope's credential and the job continues by itself. You can also select **Resume**.

<!-- VERIFY: exact banner wording and the Resume button (screenshot KU-11). -->

## Ask AI about a job

The **Ask AI** panel on the job page answers questions about the job and the cluster. It can run read-only commands on its own. Anything that could change the cluster or AWS needs your approval in the panel. See [Permissions and Safety](permissions-and-safety.md) for what is shared with the AI.

## After the upgrade

Review the job result and the audit log. Replace any standalone EC2 nodes yourself; they are listed in the plan but never touched by the job.
