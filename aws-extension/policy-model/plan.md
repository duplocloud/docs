---
description: >-
  An AWS account-level catalog of hosted zones, ACM certificates, and AMIs
  that Environments and workloads can reference.
---

# Plan

A Plan catalogs AWS account-level resources that are shared across Environments — Route 53 hosted zones, ACM certificates, and AMIs. Rather than re-discovering these resources every time they are needed, a Plan captures them once and makes them available to any Environment that references the Plan.

Plans are associated with Environments at creation time. A single Plan can be referenced by multiple Environments.

## Spec

| Field | Description |
|---|---|
| **Region** | The AWS region to catalog resources from |
| **Network Baseline** | The Network Baseline associated with this Plan. Used to scope the resource discovery to the right AWS account and region |

## Result

Once provisioned, the Plan result includes:

| Field | Description |
|---|---|
| **Primary Hosted Zone** | The primary Route 53 hosted zone for DNS configuration (hosted zone ID and domain name) |
| **Certificates** | ACM certificates available in the region, with their ARNs and domain names |
| **AMIs** | AMIs available for use in this region, with their IDs, names, and descriptions |

## Dependencies

A Plan is linked to a **Network Baseline** for region and account context. Plans are referenced by **Environments** — an Environment's workloads and load balancers use the Plan's hosted zones and certificates for DNS and TLS configuration.

## What's next

Return to the [Policy Model overview](README.md) or see how Plans are used when creating an [Environment](environment.md).
