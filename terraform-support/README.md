---
description: Information about working with DuploCloud's Terraform provider
cover: ../.gitbook/assets/banner dark.png
coverY: 0
---

# Terraform User Guide

## Using Terraform with DuploCloud

DuploCloud contains its own Terraform provider, which can access DuploCloud Cloud constructs such as [Infrastructure](https://docs.duplocloud.com/docs/getting-started/application-focussed-interface/infrastructure) and [Tenant](https://docs.duplocloud.com/docs/getting-started/application-focussed-interface/tenant). When you run DuploCloud, you’re already speeding up the creation of DevOps components, so adding another accelerator based on Terraform is a win-win proposition: less code, less maintenance, faster deployments, and faster time-to-market.

For example, you can create virtually hundreds of cloud components, from VPCs to Route tables, to subnets, with only two to three inputs in DuploCloud. Name your Infrastructure, select a region, specify a VPC CIDR, and you’re up and running in less than half an hour. Advanced configuration options such as custom endpoints are also available, among others, for fine-tuning, but only if you need them.&#x20;

Further protection is supplied by the DuploCloud Tenant, an isolated workspace that acts as an additional layer of isolation, ideal for segregating production workloads or creating extensible developer sandboxes. A Tenant’s architecture is abstracted from its underlying Infrastructure, and you can create as many Tenants as you need with no degradation in performance.&#x20;

By default, all resources within a Tenant have access to each other — a built-in feature of the DuploCloud architecture and a significant benefit to the user. For example, a Kubernetes Pod automatically has IAM access to an S3 bucket within the same tenant. Conversely, a Pod in Tenant A cannot access any resources in Tenant B unless explicitly enabled.&#x20;

However, you can explicitly enable sharing resources between Tenants, such as storage buckets and databases — even the entire Tenant itself. Clone Tenants with the [DuploCloud Terraform Exporter](https://docs.duplocloud.com/docs/aws/terraform-support/duplocloud-terraform-exporter). As with everything in DuploCloud, the controls are in your hands, not those of a third party.

The following utilities are available to manage Terraform for DuploCloud

* [DuploCloud Terraform Provider](duplocloud-terraform-provider.md)
* [DuploCloud Terraform Exporter](duplocloud-terraform-exporter/)

{% hint style="warning" %}
See how [recently updated Terraform license changes](https://duplocloud.com/blog/terraform-license-change-impacts-devops/) may impact your DevOps. If needed, contact HashiCorp, Inc. support usage is in compliance.&#x20;
{% endhint %}
