# Tenant

## Tenant as a Logical Concept

A Tenant is the most fundamental construct in DuploCloud which is essentially like a project or a workspace and is a child of the Infrastructure. While Infrastructure is a VPC level isolation, Tenant is the next level of isolation implemented by segregating Tenants using Security Groups, IAM role, Instance Profile, K8S Namespace, KMS Key, etc., in the case of AWS. Similar concepts are leveraged from other cloud providers like resource groups, managed identity, ASG, etc., in Azure.

For instructions to create a Tenant in the DuploCloud Portal, see:

* [AWS Tenant](../../../overview/use-cases/tenant-environment/)
* [Azure Tenant](../../../overview-2/use-cases/tenant-environment/)
* [GCP Tenant](../../../overview-1/use-cases/tenant-environment/)

\
A Tenant is fundamentally four things, at the logical level:

* _Container of resources_: All resources (except ones corresponding to infrastructure) are created within the Tenant. If we delete the Tenant then all resources within it are terminated.
* _Security Boundary_: All resources within the Tenant can talk to each other. For example, a Docker container deployed in an EC2 instance within the Tenant will have access to S3 buckets and RDS instances in the same Tenant. RDS instances in another Tenant cannot be reached, by default. Tenants can expose endpoints to each other via ELBs or explicit inter-tenant SG and IAM policies.
* _User Access Control:_ Self-service is the bedrock of the DuploCloud platform. To that end, users can be granted Tenant-level access. For example, Joe is an administrator who has access to all Tenants, while John and Jim are developers who can only access the Dev Tenant and Anna is a data scientist who has access only to the data science Tenant.
* _Billing Unit:_ Since a Tenant is a container of resources, all resources in the Tenant are tagged with the Tenant's name in the cloud provider, making it easy to segregate usage by Tenant.
* _Mechanism for Alerting:_ All alerts represent Faults in any resource within the Tenants.
* _Mechanism for Logging:_ Each Tenant has its unique set of logs.
* _Mechanism for metrics:_ Each Tenant has its unique set of metrics.

## Tenants and Kubernetes&#x20;

When you create Tenants in an Infrastructure, a namespace is created in the Kubernetes cluster with the name `duploservices-TENANT_NAME.`

Each Tenant is mapped to a Namespace in Kubernetes. For example, if a Tenant is called **Analytics** in DuploCloud, the Kubernetes Namespace is called `duploservices-analytics`.&#x20;

All application components within the Analytics Tenant are placed in the `duploservices-analytics` namespace. Since nodes cannot be part of a Kubernetes Namespace, DuploCloud creates a `tenantname` label for all the nodes that are launched within the Tenant. For example, a node launched in the Analytics Tenant is labeled `tenantname: duploservices-analytics`.&#x20;

Any Pods that are launched using the DuploCloud UI have an appropriate Kubernetes `nodeSelector` that ties the Pod to the nodes within the Tenant. If you are deploying via `kubectl,` ensure that your deployment is using the proper `nodeSelector`.

## Tenant use cases

Many DuploCloud customers create at least two Tenants for both their production and non-production cloud environments (Infrastructures).&#x20;

You can map Tenants in each or all of your development, testing, staging, Quality Assurance (QA), and production environments.&#x20;

For example:

* Production Infrastructure &#x20;
  * Pre-production Tenant - for preparing or reviewing production code
  * Production Tenant - for deploying tested code&#x20;
* Non-production Infrastructure
  * Development Tenant - for writing and reviewing code
  * Quality Assurance Tenant - for automated testing

In larger organizations, some customers create Tenants based on application environments, such as creating a tenant for Data Science applications, another for web applications, etc.&#x20;

Tenants are sometimes created to isolate a single customer workload, allowing more granular monitoring of performance, the flexibility of scaling, or tighter security. This is referred to as a single-Tenant setup. In this case, a DuploCloud Tenant maps to an environment used exclusively by the end client. &#x20;

When you have a large set of applications that different teams access, it is helpful to map Tenants to team workloads. For example, you could create Tenants for **Dev-analytics**, **Stage-analytics**, and so on.

