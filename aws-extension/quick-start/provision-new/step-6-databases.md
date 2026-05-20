---
description: Add a managed database to your Environment — RDS or ElastiCache.
---

# Step 6: Add Databases

With your Environment and workloads running, you can add managed databases. Databases are provisioned into the private subnets of your Network Baseline using the subnet groups created during network provisioning.

{% hint style="info" %}
Screenshots and step-by-step walkthrough coming soon.
{% endhint %}

## RDS

Create a relational database — MySQL, PostgreSQL, Aurora, or others — inside the Environment. The agent provisions the database instance, applies the Environment's security groups, and returns the connection endpoint.

## ElastiCache

Create a Redis or Memcached cluster for caching and session management. ElastiCache is provisioned into the private subnets and is accessible from workloads within the Environment.

## What's next

Your infrastructure is fully provisioned. From here you can:

* Explore [Use Cases](../../use-cases/README.md) for common operational workflows
* [Customize the extension](../../customizing/README.md) with your own skill overrides
* Connect additional environments or accounts
