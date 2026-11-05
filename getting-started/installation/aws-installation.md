---
description: What Cloud Deploys needs from your AWS account and what it creates there.
---

# AWS

AWS is the cloud Cloud Deploys supports today. This page lists what you need in your AWS account and what gets created. The steps themselves are in [Deploy Your Portal to Your Cloud](README.md).

{% hint style="info" %}
Cloud Deploys is in preview and has not been released yet.
{% endhint %}

***

## Prerequisites

| Item | Notes |
| --- | --- |
| **A connected AWS provider** | Attached to your workspace in the DevKit. See [Amazon Web Services (AWS)](../integrating-providers/amazon-web-services-aws.md). |
| **Permissions** | The provider's IAM identity must be able to create and manage VPC, EKS, IAM, S3, EFS, ACM and Route 53 resources. A dedicated, empty account is the simplest place to start, but any account works. |
| **A region** | Everything is created in the region you choose. |
| **Two hostnames** | One for the portal and one for the terminal, for example `helpdesk.example.com` and `xterm-helpdesk.example.com`. |
| **A Route 53 hosted zone or an ACM certificate** | A hosted zone that contains the hostnames, or an ACM certificate that covers both. A different DNS provider also works, and you add the records yourself. |
| **Capacity for the cluster** | The recommended cluster uses two worker nodes. The default worker size is `t3a.large`. |

You do not need to share AWS credentials with DuploCloud. Cloud Deploys uses the provider you connected in your own DevKit.

***

## What is created

| Resource | Notes |
| --- | --- |
| VPC | Public and private subnets in three zones, with a NAT gateway. |
| EKS cluster | With a managed node group. |
| EFS file system | Mount targets in the private subnets. |
| S3 buckets | For files and user data. |
| ACM certificate | For both hostnames. |
| Route 53 records | Only when you choose Route 53 mode. |
| Cluster add-ons | AWS Load Balancer Controller, EFS CSI driver, external-dns (Route 53 mode only) and the `ai-studio-efs` storage class. |
| The portal | Installed with its Helm chart in the `helpdesk` namespace, with IAM roles for its services. |
| State bucket | `duplo-helpdesk-tfstate-<account ID>`: private, versioned and encrypted. |

You can adopt an existing VPC, EKS cluster, EFS file system, S3 bucket or set of add-ons instead of creating them. Adopted resources are never modified. See [Use your existing network or cluster](README.md#use-your-existing-network-or-cluster).

***

## The Terraform behind it

Cloud Deploys runs open-source Terraform modules that DuploCloud publishes. Read the module's README for the full list of resources and variables.

TODO(link): AWS Terraform repository README (repo is being made public; master to supply the URL).
