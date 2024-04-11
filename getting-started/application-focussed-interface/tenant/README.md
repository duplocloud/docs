# Tenant

Tenant is the most fundamental construct in DuploCloud, functioning as an environment or workspace within the platform. It is essentially like a project and is a child of the infrastructure. While Infrastructure provides VPC level isolation, Tenant offers the next level of isolation. This is achieved by segregating Tenants using various mechanisms such as Security Groups (SG), IAM roles, Instance Profiles, K8S Namespaces, KMS Keys, etc., in the context of AWS. Similar concepts apply to other cloud providers, leveraging resource groups, managed identities, ASG, etc., in Azure.

A Tenant in DuploCloud encapsulates several key aspects at the logical level:

* _Container of resources_: It serves as a container where all resources (except those corresponding to infrastructure) are created and managed. Deleting a tenant results in the termination of all contained resources.
* _Security Boundary_: It acts as a security boundary within which all resources can interact with each other. For instance, a Docker container deployed in an EC2 instance within the tenant will have access to S3 buckets and RDS instances also within the tenant. However, it cannot access RDS instances in another tenant by default. Tenants can, however, expose endpoints to each other through ELBs or by setting up explicit inter-tenant SG and IAM policies.
* _User Access Control_: DuploCloud emphasizes self-service, allowing users to be granted Tenant level access. This enables a flexible and secure access control model where, for example, developers John and Jim may have access to the Dev tenant, Joe has administrative access across all tenants, and Anna, a data scientist, has access only to the Data Science tenant.
* _Billing Unit_: As a container of resources, each Tenant's resources are tagged with the Tenant's name by the cloud provider. This facilitates easy segregation of usage and billing by tenant, simplifying financial management and reporting.

{% hint style="info" %}
A common use case for Tenant in an organization might involve multiple tenants such as Dev and QA under the non-prod infrastructure, with Pre-prod and Prod tenants under the Prod Infrastructure. In larger organizations, tenants might be organized by functional groups, such as one for Data Science and another for web applications. Some companies create dedicated tenants for each of their end-user clients in scenarios where the application is single-tenant. This flexibility underscores the Tenant's role as a logical concept adaptable to various organizational structures and needs.
{% endhint %}

In essence, a DuploCloud tenant is designed to provide an isolated environment that encompasses security, resource management, user access control, and billing, tailored to the specific needs of different projects or workspaces within an organization.