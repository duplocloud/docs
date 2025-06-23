---
description: Information about working with DuploCloud's Pulumi provider
---

# Pulumi User Guide

## Using Pulumi with DuploCloud

DuploCloud supports the use of Pulumi, a modern Infrastructure as Code (IaC) tool that enables you to manage infrastructure using general-purpose programming languages like Python, TypeScript, Go, and C#. DuploCloud’s Pulumi provider extends Pulumi’s reach to cover DuploCloud-managed constructs  including Infrastructure, Tenants, Services, and more.

Pulumi brings the speed and flexibility of real programming languages to the infrastructure space. Combined with DuploCloud’s rapid provisioning capabilities, it offers a powerful, programmatic way to deploy full-stack cloud environments with minimal overhead.

For example, you can deploy entire application stacks, complete with Kubernetes workloads, IAM permissions, and cloud services, using just a few lines of Pulumi code. Define your infrastructure once, reuse it across environments, and push updates directly from CI/CD pipelines using native Pulumi tooling.

Additionally, DuploCloud’s multi-tenant architecture is preserved through Pulumi. Each Tenant remains a secure, isolated workspace, enabling clean separation between production, staging, and development workloads. Just like in the DuploCloud UI, all resources within a Tenant have default access to one another, simplifying permission management for common use cases such as allowing a Kubernetes service to access an S3 bucket or database in the same environment.

Pulumi is well-suited for DuploCloud environments that require cross-tenant access and resource sharing. It offers explicit control over shared infrastructure components, allowing infrastructure engineers to design flexible systems and enabling application developers to safely reuse infrastructure using familiar programming languages.

The DuploCloud Pulumi provider supports:

* Python
* TypeScript / JavaScript
* Go
* C# / .NET

The following utilities are available to manage Pulumi for DuploCloud:

* DuploCloud Pulumi Provider
* [DuploCloud Terraform & Pulumi Examples](https://github.com/duplocloud/terraform-provider-duplocloud/tree/main/examples)
