---
description: >-
  Provision or import the network that everything else runs on: a VPC on AWS,
  a VNet on Azure, or a VCN on Oracle Cloud.
---

# Network Baseline

A Network Baseline is the networking foundation of your infrastructure. Every Cluster and Environment depends on one. It's the first resource you create when building new infrastructure from scratch.

When you create a Network Baseline, you choose its **Cloud**: **AWS**, **Azure**, or **Oracle Cloud (OCI)**. Everything you build on the network uses that cloud.

| Cloud | What the Network Baseline creates |
| --- | --- |
| **AWS** | A VPC with public and private subnets across availability zones, internet and NAT gateways, route tables, and optional VPC flow logs |
| **Azure** | A VNet in its own resource group, with subnets, a network security group per subnet, and NAT gateways |
| **Oracle Cloud (OCI)** | A VCN and its subnets |

## Spec on AWS

{% hint style="info" %}
The fields below are for **AWS**. Azure and Oracle Cloud (OCI) use the same resource with their own fields. Their details are coming soon.
{% endhint %}


| Field | Description |
|---|---|
| **Region** | The AWS region where the VPC will be created |
| **CIDR** | The IP address range for the VPC (e.g. `10.0.0.0/16`) |
| **Availability Zones** | Number of AZs to span (1–4). Each AZ gets one public and one private subnet |
| **Subnet Prefix** | The subnet size within the VPC (e.g. `/24`) |
| **NAT Mode** | How private subnets reach the internet: **None** (no NAT), **Single AZ** (one shared NAT gateway), or **Multi AZ** (one NAT gateway per AZ for high availability) |
| **DNS** | Enable DNS resolution and DNS hostnames within the VPC |
| **VPC Flow Logs** | Capture and store network traffic metadata for auditing and analysis |
| **Mode** | **Create** — provision a new VPC. **Import** — attach an existing VPC without creating any new AWS resources |

## Result on AWS

Once provisioned, the Network Baseline result includes:

| Field | Description |
|---|---|
| **VPC** | The VPC ID and CIDR block |
| **Internet Gateway** | The internet gateway attached to the VPC |
| **Subnets** | Public and private subnets, one pair per availability zone, with CIDR and AZ details |
| **NAT Gateways** | NAT gateways (if enabled), with their associated public IP addresses |
| **Route Tables** | Public and private route tables |
| **Flow Logs** | Flow log ARN (if enabled) |
| **RDS Subnet Groups** | Pre-created subnet groups for RDS databases (public and private tiers) |
| **ElastiCache Subnet Group** | Pre-created subnet group for ElastiCache clusters |

## Dependencies

A Network Baseline has no dependencies — it is the root of the resource hierarchy. However, a Network Baseline cannot be deprovisioned while Clusters depend on it.

## Import Mode

If you already have a network, use **Import** mode to attach it to the Infrastructure Agent. On AWS, the platform discovers the existing VPC's subnets, route tables, NAT gateways, and internet gateway without creating or modifying any resources. Azure and OCI networks can be imported the same way. Once imported, the network appears in the agent like any provisioned resource — Clusters and Environments can be built on top of it.

{% hint style="warning" %}
Imported networks cannot be deprovisioned through the Infrastructure Agent.
{% endhint %}

## What's next

With a Network Baseline provisioned, create a [Cluster Baseline](cluster-baseline.md) to run a Kubernetes cluster on top of it.
