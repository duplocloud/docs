---
description: Create a Network Baseline — a VPC with public and private subnets across multiple availability zones.
---

# Step 1: Create a Network

A Network Baseline provisions the VPC that all other resources will run inside. This is the first resource you create.

{% hint style="info" %}
Screenshots and step-by-step walkthrough coming soon.
{% endhint %}

## What gets created

* A VPC with your chosen CIDR block
* Public and private subnets, one pair per availability zone
* An Internet Gateway for public subnet routing
* NAT Gateways for private subnet outbound access (if enabled)
* Route tables for public and private subnets
* RDS and ElastiCache subnet groups pre-configured for databases

## Next step

Once the Network Baseline status shows **Ready**, proceed to [Step 2: Create a Cluster](step-2-cluster.md).
