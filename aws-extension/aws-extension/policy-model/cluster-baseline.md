---
description: Provision an AWS EKS cluster on top of a Network Baseline.
---

# Cluster Baseline

A Cluster Baseline provisions an AWS EKS cluster. It is the compute layer that sits on top of a Network Baseline, and it is the parent of all Environments — each Environment runs inside a Cluster.

## Spec

| Field | Description |
|---|---|
| **Network Source** | The Network Baseline to build on top of. The VPC, region, and subnets are inherited automatically. You can also provide a VPC and subnets directly if not using a managed Network Baseline |
| **Cluster Type** | **Standard** — a standard EKS cluster where you manage node groups. **Auto** — EKS Auto Mode, where AWS manages the compute layer automatically |
| **EKS Version** | The Kubernetes version to deploy (e.g. `1.31`) |
| **API Server Visibility** | Whether the Kubernetes API endpoint is **Public**, **Private**, or **Public and Private** |
| **Control Plane Logging** | Which EKS control plane log types to enable: API, Audit, Authenticator, Controller Manager, Scheduler |
| **Cluster IP CIDR** | The IP range used internally by Kubernetes for service IP assignment (e.g. `172.20.0.0/16`) |

## Result

Once provisioned, the Cluster Baseline result includes:

| Field | Description |
|---|---|
| **Cluster ARN** | The unique ARN of the EKS cluster |
| **API Endpoint** | The URL of the Kubernetes API server |
| **OIDC Issuer URL** | Used for IAM Roles for Service Accounts (IRSA) |
| **Certificate Authority** | The cluster's certificate authority data |

{% hint style="success" %}
After provisioning, a Kubernetes Provider and Scope are automatically created for the cluster. The AI agent can immediately begin managing Kubernetes resources inside it without any additional setup.
{% endhint %}

## Dependencies

A Cluster Baseline requires a **Network Baseline** (or equivalent VPC and subnet configuration). A Cluster cannot be deprovisioned while Environments depend on it.

## What's next

With a Cluster Baseline provisioned, create an [Environment](environment.md) as a deployment boundary inside it.
