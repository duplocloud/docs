---
description: Build new AWS infrastructure from scratch — Network, Cluster, Plan, Environment, Workloads, and Databases.
---

# Provision New Infrastructure

This guide walks through creating a complete AWS environment from scratch using the AWS Extension — from the VPC network up to running workloads and managed databases.

## What you will build

By the end of this guide, you will have:

* A **Network Baseline** — a VPC with public and private subnets across multiple availability zones
* A **Cluster Baseline** — an EKS cluster running inside that network
* A **Plan** — an account-level catalog of hosted zones, certificates, and AMIs
* An **Environment** — a deployment boundary inside the cluster with dedicated IAM and security group isolation
* **Workloads** — a running application deployed into the Environment
* **Databases** — a managed RDS or ElastiCache instance

## Steps

{% stepper %}
{% step %}
## [Create a Network](step-1-network.md)

Provision a VPC with public and private subnets across multiple availability zones, NAT gateways, and RDS/ElastiCache subnet groups.
{% endstep %}

{% step %}
## [Create a Cluster](step-2-cluster.md)

Provision an EKS cluster inside your Network Baseline. Choose Standard or Auto Mode depending on your workload requirements.
{% endstep %}

{% step %}
## [Create a Plan](step-3-plan.md)

Create an account-level catalog of Route 53 hosted zones, ACM certificates, and AMIs that your Environments will reference.
{% endstep %}

{% step %}
## [Create an Environment](step-4-environment.md)

Create a deployment boundary inside your cluster with dedicated security groups, IAM roles, and KMS keys. Attach your Plan to make hosted zones and certificates available to workloads.
{% endstep %}

{% step %}
## [Deploy Workloads](step-5-workloads.md)

Create a Namespace and deploy a containerized application into your Environment. Optionally attach a load balancer to expose the application externally.
{% endstep %}

{% step %}
## [Add Databases](step-6-databases.md)

Provision a managed RDS or ElastiCache instance into the private subnets of your Network Baseline. Databases are immediately accessible from workloads in the same Environment.
{% endstep %}
{% endstepper %}

## Prerequisites

* DuploCloud is installed and running. See [Installation](../../installation/README.md).
* An AWS Provider with write access to your AWS account is connected. See [Integrating Providers](../../../getting-started/integrating-providers/README.md).
* A Workspace has been created with the AWS Provider scope attached.
