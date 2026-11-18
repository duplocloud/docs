---
description: Activate the Kubernetes Upgrade agent from the Agent Marketplace, connect it to an Amazon EKS cluster, and get an upgrade plan without changing anything.
---

# Try a Marketplace Agent

In this step you activate a ready-made agent, **Kubernetes Upgrade**, and use it to plan an upgrade of an Amazon EKS cluster. You'll see which versions you can move to, which add-ons need updating, and what could go wrong, all before anything in the cluster changes.

Everything on this page is read-only. The agent only changes a cluster after someone approves a plan, and you'll reject the plan at the end.

{% hint style="info" %}
Kubernetes Upgrade works with **Amazon EKS** clusters. If you don't use EKS, skip ahead to [Build Your Own Agent](build-your-own-agent/README.md) and pick your platform there.
{% endhint %}

## What you need

* The DevKit running, and signed in as the admin user. See [Install the DevKit](install-the-devkit.md).
* An AWS account with an EKS cluster in it. Any cluster works, since you won't change it.
* AWS credentials that can read the cluster. The policy below is enough for this walkthrough.

<details>

<summary>Read-only IAM policy for this walkthrough</summary>

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "KubernetesUpgradePlanReadOnly",
      "Effect": "Allow",
      "Action": [
        "sts:GetCallerIdentity",
        "ec2:DescribeRegions",
        "ec2:DescribeInstances",
        "ec2:DescribeInstanceTypes",
        "ec2:DescribeSubnets",
        "eks:ListClusters",
        "eks:DescribeCluster",
        "eks:DescribeClusterVersions",
        "eks:ListInsights",
        "eks:ListAddons",
        "eks:DescribeAddon",
        "eks:DescribeAddonVersions",
        "eks:ListNodegroups",
        "eks:DescribeNodegroup",
        "autoscaling:DescribeAutoScalingGroups",
        "servicequotas:GetServiceQuota",
        "servicequotas:GetAWSDefaultServiceQuota"
      ],
      "Resource": "*"
    }
  ]
}
```

If a read permission is missing, the affected check shows **Unverified** instead of failing, so you can still finish the walkthrough.

</details>

## 1. Connect your AWS account

Add your AWS account as a provider, then attach its scope to your workspace. See [Connecting Providers: Amazon Web Services (AWS)](integrating-providers/amazon-web-services-aws.md).

## 2. Activate Kubernetes Upgrade

{% stepper %}
{% step %}
### Open the Agent Marketplace

Go to **AI Admin → Agents** and open the **Agent Marketplace** tab.
{% endstep %}

{% step %}
### Activate the agent

Find **Kubernetes Upgrade** and click **Activate**.
{% endstep %}

{% step %}
### Choose where it appears

The portal asks **Where should it appear in your left nav?** Keep the recommended section, or pick another one, then choose its position. Your choice is kept when the agent is upgraded, and you can change it any time in the Marketplace.
{% endstep %}

{% step %}
### Wait for it to install

Progress shows on the page. It usually takes under a minute. When it finishes, the agent appears in your left nav under **Kubernetes Upgrader**.
{% endstep %}
{% endstepper %}

## 3. Add your EKS cluster

1. In the left nav, open **Kubernetes Upgrader → Kubernetes Clusters**.
2. Click **Add Kubernetes Cluster**.
3. Fill in the form. Each field appears once the one before it is filled:
   * **Name**: a name for the cluster in DuploCloud.
   * **Scope**: the AWS scope you attached in step 1.
   * **Region**: the region your cluster is in.
   * **Kubernetes Cluster**: pick your cluster from the list the agent found.
4. Click **Create**.

The agent only reads your account to find the cluster.

## 4. Plan an upgrade

1. Open the cluster and click **Add Upgrade Job**.
2. Enter a **Name** for the job.
3. Tick **Upgrade EKS control plane version** and choose a **Target K8s Version**. Each option shows how many steps it takes and whether it uses extended support.
4. If your cluster uses EKS add-ons, tick **Upgrade EKS add-ons** to see which add-ons will move to which version. If it doesn't, skip this.
5. Look at **Upgrade Path**. It lists every step the job would run, plus any blockers and warnings.
6. Click **Create plan**.

Creating a plan runs pre-flight checks: EKS upgrade insights, add-on compatibility, container image availability, and EC2 quota and subnet IPs. Nothing in the cluster changes yet.

## 5. Review the plan, then reject it

The job page shows **Review & approve the upgrade plan**, with:

* the upgrade path, step by step
* each add-on's current and target version, if you chose to upgrade add-ons
* the result of every pre-flight check
* whether DuploCloud can reach the cluster, and which permissions it has

This is the agent's result: a full, checked plan for your upgrade.

To finish the walkthrough without changing anything, click **Reject**. If you do nothing, the plan expires after 5 minutes and is cancelled on its own.

{% hint style="danger" %}
Don't click **Approve & start upgrade** on a cluster you care about. Approving upgrades the control plane, which **can't be undone**, and can drain and replace worker nodes.
{% endhint %}

## What you just did

You activated an agent from the Marketplace, connected it to your AWS account, and used it to plan a change safely. Every Marketplace agent follows the same pattern: activate it, connect it, and review what it proposes before it acts.

To learn more about this agent, including running a real upgrade, see [Kubernetes Upgrade](../marketplace-agents/kubernetes-upgrade/README.md).

**Next step in the Quick Start:** [Build Your Own Agent](build-your-own-agent/README.md).
