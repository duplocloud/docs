---
description: Create a Cluster Baseline — an EKS cluster built on top of your Network Baseline.
---

# Step 2: Create a Cluster

A Cluster Baseline provisions an EKS cluster inside the Network you created in the previous step. The VPC, region, and subnets are inherited automatically from the Network Baseline.

{% hint style="info" %}
Screenshots and step-by-step walkthrough coming soon.
{% endhint %}

## What gets created

* An EKS cluster with your chosen Kubernetes version
* Cluster IAM role and service account configuration
* OIDC provider for IAM Roles for Service Accounts (IRSA)
* A Kubernetes Provider and Scope automatically connected to the new cluster

## Next step

Once the Cluster Baseline status shows **Ready**, proceed to [Step 3: Create an Environment](step-3-environment.md).
