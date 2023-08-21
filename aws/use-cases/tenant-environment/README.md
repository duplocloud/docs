---
description: Using Tenants in DuploCloud
---

# Tenant (Environment)

In AWS, cloud features such as AWS resource groups, AWS IAM, AWS security groups, KMS keys, as well as Kubernetes Namespaces, are exposed in Tenants which reference their configurations.

When you create Tenants in an Infrastructure, a namespace is created in the Kubernetes cluster with the name `duploservices-TENANT_NAME.`

Each [Tenant ](broken-reference)is mapped to a Namespace in Kubernetes. For example, if a Tenant is called **Analytics** in DuploCloud, the Kubernetes Namespace is called `duploservices-analytics`.&#x20;

All application components within the Analytics Tenant are placed in the `duploservices-analytics` namespace. Since nodes cannot be part of a Kubernetes Namespace, DuploCloud creates a `tenantname` label for all the nodes that are launched within the Tenant. For example, a node launched in the Analytics Tenant is labeled`tenantname: duploservices-analytics`.&#x20;

Any Pods that are launched using the DuploCloud UI have an appropriate Kubernetes `nodeSelector` that ties the Pod to the nodes within the Tenant. If you are deploying via `kubectl,`ensure that your deployment is using the proper `nodeSelector`.

![](<../../../.gitbook/assets/image (16) (3).png>)

At the logical level, the Tenant is:

* **A Container of resources**: All resources (except ones corresponding to the Infrastructure) are created within the Tenant. If a tenant is deleted, all the resources in the Tenant are terminated.
* **A Security Boundary:** All resources within a Tenant can talk to each other. For example, a Docker container deployed in an EKS instance within the tenant will have access to S# storage and RDS databases within the same tenant. RDS database instances in another tenant cannot be reached, for example, by default. Tenants expose endpoints to each other using load balancers or explicit inter-Tenant security groups and identity management policies.
* **User Access Control:** Self-service is the bedrock of the DuploCloud platform. To that end, users can be granted Tenant level access. For example, John and Jim are developers who can be granted access to the **DEV01** tenant, Joe is an administrator who has access to all tenants, and Anna is a data scientist who has access _only_ to the **DATASCI** tenant.
* **A Billing Unit**: Because the Tenant is a container of resources, all resources in the Tenant are tagged with the Tenant's name in the cloud provider, making it easy to segregate usage by Tenant.
* **A mechanism for alerting**: All alerts represent Faults in any resource within the Tenants.
* **A mechanism for logging**: Each Tenant has its unique set of logs.
* **A mechanism for metrics:** Each Tenant has its unique set of metrics.

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

Tenants are sometimes created to isolate a single customer workload, allowing more granular monitoring of performance, the flexibility of scaling, or tighter security. This is referred to as a _single-Tenant_ setup. In this case, a DuploCloud Tenant maps to an environment used exclusively by the end client. &#x20;

When you have a large set of applications that different teams access, it is helpful to map Tenants to team workloads. For example, you could create Tenants for **Dev-analytics**, **Stage-analytics**, and so on.

### Tenant abstraction and isolation

While Infrastructure provides abstraction and isolation at the Virtual Private Cloud (VPC) and Kubernetes level, the Tenant supplies the next level of isolation implemented in EKS by segregating Tenants using the following construct _per_ Tenant

* A set of security groups
* An identity management role and profile
* A Kubernetes Namespace, a read-only service account, and a write service account
* KMS Key
* PEM file

EKS Worker nodes or virtual machines (VMs) created within a Tenant are given a label with the Tenant Name, as are the node selectors and namespaces. Consequently, even at the worker node level, two tenants achieve complete isolation and independence, even though they may be sharing the same Kubernetes cluster by a shared Infrastructure.

## Creating a Tenant <a href="#2-toc-title" id="2-toc-title"></a>

To add a Tenant, navigate to **Administrator** -> **Tenant** in the DuploCloud Portal and click **Add**.

Each [Tenant ](broken-reference)is mapped to a Namespace in Kubernetes. For example, if a Tenant is called **Analytics** in DuploCloud, the Kubernetes Namespace is called `duploservices-analytics`.&#x20;

All application components within the Analytics Tenant are placed in the `duploservices-analytics` namespace. Since nodes cannot be part of a Kubernetes Namespace, DuploCloud creates a `tenantname` label for all the nodes that are launched within the Tenant. For example, a node launched in the Analytics Tenant is labeled`tenantname: duploservices-analytics`.&#x20;

Any Pods that are launched using the DuploCloud UI have an appropriate Kubernetes `nodeSelector` that ties the Pod to the nodes within the Tenant. If you are deploying via `kubectl,`ensure that your deployment is using the proper `nodeSelector`.
