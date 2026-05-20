---
description: Create an Environment — a deployment boundary inside your cluster with dedicated IAM and network isolation.
---

# Step 4: Create an Environment

An Environment is a deployment boundary inside the Cluster you created in Step 2. It provisions dedicated security groups, IAM roles, and KMS keys scoped to this environment. Attaching the Plan you created in Step 3 makes its hosted zones and certificates available to workloads and load balancers in this Environment.

{% hint style="info" %}
Screenshots and step-by-step walkthrough coming soon.
{% endhint %}

## What gets created

* Security groups controlling inbound and outbound traffic for resources in this Environment
* IAM roles scoped to the Environment for workloads and service accounts
* KMS encryption keys for secrets and storage

## Next step

Once the Environment status shows **Ready**, proceed to [Step 5: Deploy Workloads](step-5-workloads.md).
