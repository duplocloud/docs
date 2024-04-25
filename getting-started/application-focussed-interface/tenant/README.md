# Tenant

Tenant is the most fundamental construct in DuploCloud, acting as a project or workspace and is a child of the infrastructure. It represents an application's entire lifecycle and is designed to provide a high degree of isolation and security. While Infrastructure is a VPC level isolation, Tenant is the next level of isolation implemented by leveraging security mechanisms such as Security Groups, IAM roles, Instance Profiles, and K8S Namespaces in AWS, with analogous concepts like resource groups and managed identities in Azure.

\
A Tenant in DuploCloud is fundamentally four things, at the logical level:

* _Container of resources_: All resources (except those corresponding to infrastructure) are created within the Tenant. Deleting the tenant results in the termination of all contained resources. It acts as a container for resources, security boundaries, user access control mechanisms, billing units, alerting mechanisms, logging mechanisms, and metric tracking units, ensuring a comprehensive management and operational framework.

* _Security Boundary_: It serves as a security boundary with unique security groups, IAM roles, and instance profiles per tenant, ensuring that all resources within the tenant can communicate with each other securely. For instance, a Docker container deployed in an EC2 instance within the tenant will have access to S3 buckets and RDS instances within the same tenant, but not to those in another tenant, unless explicitly allowed through inter-tenant security group (SG) and IAM policies.

* _User Access Control_: DuploCloud emphasizes self-service, allowing users to be granted Tenant level access based on their roles. For example, developers John and Jim may have access to the Dev tenant, while Joe, an administrator, has access to all tenants, and Anna, a data scientist, has access only to the data science tenant. This granularity in access control facilitates efficient and secure collaboration across different teams and projects.

* _Billing Unit_: As a billing unit, the Tenant simplifies financial management by tagging all resources with the Tenant's name in the cloud provider. This feature makes it easy to segregate and track usage by tenant, aiding in cost allocation and budgeting.

{% hint style="info" %}
A common use case for Tenant in an organization includes having multiple tenants such as Dev and QA under the non-prod infrastructure, and Pre-prod and Prod tenants under the Prod Infrastructure. In larger organizations, tenants can be organized by groups, such as a tenant for Data Science and another for web applications. Some companies create dedicated tenants for each of their end-user clients in scenarios where the application is single-tenant. This flexibility demonstrates that Tenant is a logical concept adaptable to various organizational structures and operational strategies.
{% endhint %}

Tenants are instrumental in isolating customer workloads, which allows for granular performance monitoring, scaling flexibility, and enhanced security. They also facilitate the isolation of environments, making it possible to manage applications throughout their lifecycle efficiently.

\
**Related Resources:**  
1. [Getting Started with Tenant in DuploCloud](https://docs.duplocloud.com/docs/getting-started/application-focussed-interface/tenant)  
2. [Tenant Environment Use Cases in GCP](https://docs.duplocloud.com/docs/gcp/use-cases/tenant-environment)  
3. [Tenant Environment Use Cases in AWS](https://docs.duplocloud.com/docs/aws/use-cases/tenant-environment/)  
4. [Tenant Environment Use Cases in Azure](https://docs.duplocloud.com/docs/azure/use-cases/tenant-environment)