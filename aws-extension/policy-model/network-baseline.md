---
description: >-
  Provision or import a well-architected AWS VPC network that serves as the
  foundation for your cloud infrastructure.
---

# Network Baseline

A Network Baseline is the networking foundation of your AWS infrastructure. It provisions a VPC with public and private subnets spread across multiple availability zones, along with internet gateways, NAT gateways, route tables, and optional VPC flow logs.

Every Cluster and Environment depends on a Network Baseline. It is the first resource you create when building new AWS infrastructure from scratch.

## Spec

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

## Result

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

If you already have a VPC in AWS, use **Import** mode to attach it to the AWS Extension. The platform discovers the existing VPC's subnets, route tables, NAT gateways, and internet gateway without creating or modifying any resources. Once imported, the network appears in the extension like any provisioned resource — Clusters and Environments can be built on top of it.

{% hint style="warning" %}
Imported networks cannot be deprovisioned through the AWS Extension.
{% endhint %}

## What's next

With a Network Baseline provisioned, create a [Cluster Baseline](cluster-baseline.md) to run an EKS cluster on top of it.
