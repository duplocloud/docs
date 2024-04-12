# Tenant

Tenant is the most fundamental construct in DuploCloud which is essentially like a project or a workspace and is a child of the infrastructure. While Infrastructure is a VPC level isolation, Tenant is the next level of isolation implemented by segregating Tenants using Security Groups, IAM role, Instance Profile, K8S Namespace, KMS Key, etc., in case of AWS. Similar concepts are leveraged from other cloud providers like resource groups, managed identity, ASG, etc., in Azure.

\
A Tenant is fundamentally four things, at the logical level:

* _Container of resources_: All resources (except ones corresponding to infrastructure) are created within the Tenant. If we delete the tenant then all resources within that are terminated.
* _Security Boundary_: All resources within the tenant can talk to each other. For example a Docker container deployed in an EC2 instance within the tenant will have access to S3 buckets and RDS instances within the same tenant. RDS instances in another tenant cannot be reached, by default. Tenant can expose endpoints to each other either via ELBs or explicit inter-tenant SG and IAM policies.
* _User Access Control:_ Self-service is the bedrock of the DuploCloud platform. To that end, users can be granted Tenant level access. For example John and Jim are developers who can be granted access to Dev tenant, while Joe is an administrator who has access to all tenants, while Anna is a data scientist who has access only to the data science tenant.
* _Billing Unit:_ Since Tenant is a container of resources, all resources in the tenant are tagged with the Tenant's name in the cloud provider, making it easy to segregate usage by tenant.

{% hint style="info" %}
A common use case for Tenant in an organization that contains 4 tenants: Dev and QA are under the non-prod infrastructure, while the Pre-prod and Prod tenants are under the Prod Infrastructure. In larger organizations, one could have tenants by groups as well like a tenant for Data Science, Tenant for web application, etc. We have seen companies creating dedicated tenants for each of their end user clients in cases where the application is single Tenant. Tenant is a logical concept that can be used either way.
{% endhint %}
