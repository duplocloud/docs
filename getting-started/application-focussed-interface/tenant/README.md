# Tenant

Tenant is the most fundamental construct in DuploCloud, acting as a project or workspace and is a child of the infrastructure. While Infrastructure provides VPC level isolation, Tenant offers the next level of isolation. This is achieved by segregating Tenants using Security Groups, IAM role, Instance Profile, K8S Namespace, KMS Key, etc., in the case of AWS. Similar concepts are applied in other cloud providers like resource groups, managed identity, ASG, etc., in Azure.

A Tenant in DuploCloud is a logical construct designed to encapsulate the entire lifecycle of an application, serving as a security boundary equipped with unique security groups, IAM roles, and instance profiles specific to each tenant. This design ensures that resources within a tenant can communicate securely and efficiently, isolating customer workloads for detailed performance monitoring, flexible scaling, and enhanced security measures.

\
A Tenant is fundamentally four things, at the logical level:

* _Container of resources_: All resources (except those corresponding to infrastructure) are created within the Tenant. Deleting the tenant results in the termination of all resources within it.
* _Security Boundary_: Resources within a tenant can interact with each other securely. For instance, a Docker container deployed in an EC2 instance within the tenant will have access to S3 buckets and RDS instances in the same tenant, but not to those in another tenant, by default. Tenants can expose endpoints to each other through ELBs or explicit inter-tenant SG and IAM policies.
* _User Access Control_: DuploCloud emphasizes self-service, allowing users to be granted Tenant level access. For example, developers John and Jim may have access to the Dev tenant, while administrator Joe has access to all tenants, and data scientist Anna has access only to the data science tenant.
* _Billing Unit_: As a container of resources, all resources in the tenant are tagged with the Tenant's name in the cloud provider, facilitating easy segregation of usage by tenant.

Tenants serve multiple roles, including acting as containers for resources, security boundaries, mechanisms for user access control, billing units, and systems for alerting, logging, and metric tracking. This multifaceted approach allows for effective segregation and isolation of resources within the cloud environment.

{% hint style="info" %}
A common use case for Tenant in an organization includes having 4 tenants: Dev and QA under the non-prod infrastructure, and Pre-prod and Prod tenants under the Prod Infrastructure. In larger organizations, tenants might be organized by groups, such as a tenant for Data Science, a tenant for web applications, etc. It's also common for companies to create dedicated tenants for each of their end-user clients in scenarios where the application is single-tenant. Tenant is a logical concept that can be flexibly applied to meet various organizational needs.
{% endhint %}

Related Resources for further exploration include:
1. [Getting Started with Tenants in DuploCloud](https://docs.duplocloud.com/docs/getting-started/application-focussed-interface/tenant)
2. [Tenant Environment Use Cases in GCP](https://docs.duplocloud.com/docs/gcp/use-cases/tenant-environment)
3. [Tenant Environment Use Cases in AWS](https://docs.duplocloud.com/docs/aws/use-cases/tenant-environment/)
4. [Tenant Environment Use Cases in Azure](https://docs.duplocloud.com/docs/azure/use-cases/tenant-environment)