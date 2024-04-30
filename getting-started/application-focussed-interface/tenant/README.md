# Tenant

Tenant is the most fundamental construct in DuploCloud, acting as a logical layer above the cloud infrastructure (such as AWS, GCP, or Azure) and is akin to a project or a workspace. It is a child of the infrastructure, with Infrastructure providing VPC level isolation, while Tenant offers a more granular level of isolation. This isolation is achieved through the use of Security Groups, IAM roles, Instance Profiles, K8S Namespaces, KMS Keys, etc., in AWS, with similar mechanisms like resource groups and managed identities in Azure.

A Tenant in DuploCloud represents an application's entire lifecycle and serves multiple key roles:

* _Container of resources_: It encapsulates all resources (except those tied to infrastructure) within it. Deleting a tenant results in the termination of all contained resources.
* _Security Boundary_: It acts as a security boundary with unique security groups and IAM roles, ensuring resources within a tenant can communicate freely while isolating them from resources in other tenants. For instance, a Docker container in an EC2 instance within a tenant can access S3 buckets and RDS instances in the same tenant but not those in another tenant, unless explicitly allowed through ELBs or inter-tenant security and IAM policies.
* _User Access Control_: DuploCloud emphasizes self-service, allowing specific user access at the tenant level. This means developers, administrators, and specialists like data scientists can be granted access to only the tenants relevant to their roles, enhancing both security and operational efficiency.
* _Billing Unit_: Each tenant acts as a billing unit, with all resources tagged with the tenant's name in the cloud provider. This facilitates easy segregation of usage and costs by tenant.

Tenants also enable more granular performance monitoring, scaling flexibility, and tighter security. They serve as a mechanism for alerting, logging, and metrics, ensuring that users can maintain optimal performance and security postures.

{% hint style="info" %}
A common use case for Tenant in an organization includes having separate tenants for different stages of development and production, such as Dev and QA under non-prod infrastructure, and Pre-prod and Prod under Prod Infrastructure. Larger organizations might have tenants by function, such as one for Data Science and another for web applications. It's also common for companies to create dedicated tenants for each of their end-user clients in scenarios where the application is single-tenant. This flexibility shows that Tenant is a versatile concept that can adapt to various organizational structures and needs.
{% endhint %}