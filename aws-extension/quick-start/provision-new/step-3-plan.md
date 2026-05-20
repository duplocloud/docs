---
description: Create a Plan — an account-level catalog of hosted zones, ACM certificates, and AMIs.
---

# Step 3: Create a Plan

A Plan catalogs the AWS account-level resources your environments and workloads will reference — Route 53 hosted zones for DNS, ACM certificates for TLS, and AMIs for compute. Creating a Plan before the Environment means you can attach it at Environment creation time.

{% hint style="info" %}
Screenshots and step-by-step walkthrough coming soon.
{% endhint %}

## What gets created

* A catalog of Route 53 hosted zones available in your account and region
* A list of ACM certificates with their domain names and ARNs
* A list of AMIs available for workload and host provisioning

## Next step

Once the Plan is ready, proceed to [Step 4: Create an Environment](step-4-environment.md).
