---
description: An outline of the tenancy deployment models supported by DuploCloud
---

# DuploCloud Tenancy Models

DuploCloud supports a variety of deployment models, from basic multi-tenant applications to complex single-tenant deployments within customer environments. These models cater to different security needs, allowing customers to achieve their desired isolation level while maintaining operational efficiency.&#x20;

DuploCloud-supported tenancy models, outlined below, include:

* [Application-managed multi-tenancy](duplocloud-tenancy-models.md#application-managed-multi-tenancy)
* [DuploCloud Tenant per customer](duplocloud-tenancy-models.md#duplocloud-tenant-per-customer)
* [DuploCloud Infrastructure per customer](duplocloud-tenancy-models.md#duplocloud-infrastructure-per-customer)
* [Cloud account per customer](duplocloud-tenancy-models.md#cloud-account-per-customer)
* [Hybrid model](duplocloud-tenancy-models.md#hybrid-model)
* [On-premises ](duplocloud-tenancy-models.md#special-hybrid-case-single-tenant-deployment-in-external-kubernetes-cluster)

## Tenancy deployment models

### Application-managed multi-tenancy

<figure><img src="../.gitbook/assets/1 - Application Provides Tenancy.png" alt=""><figcaption><p>DuploCloud pooled tenancy model</p></figcaption></figure>

* **Description**: The application manages tenant isolation with DuploCloud structured pooled tenancy.&#x20;
* **Use Case**: The most common scenario is where the application logic isolates customer data. DuploCloud Tenants are then used to isolate development environments (i.e., nonprod and prod).&#x20;
* **Infrastructure**:
  * Shared DuploCloud Infrastructure (VPC, Tenant, VM/instances, S3 bucket, RDS). Cluster/namespace can also be shared.&#x20;
  * Scaling: increase compute instances for Kubernetes worker nodes as needed.

### DuploCloud Tenant per customer

<figure><img src="../.gitbook/assets/2 - DuploCloud Tenant.png" alt=""><figcaption><p>DuploCloud shared cluster with separate namespace per tenant</p></figcaption></figure>

* **Description**: Each customer gets a separate DuploCloud Tenant.
* **Use Case**: Suitable for older applications not designed for multi-tenancy, or security and compliance needs.
* **Infrastructure**:
  * Shared network layer (VPC).
  * Separate Tenants per customer with security boundaries (security group, KMS key, SSH key, Kubernetes namespace).
  * Kubernetes cluster is shared and boundaries are through the namespace.

### DuploCloud Infrastructure per customer

<figure><img src="../.gitbook/assets/3 - DuploCloud Infrastructure.png" alt=""><figcaption><p>DuploCloud siloed cluster per Tenant with separate network infrastructure</p></figcaption></figure>

* **Description**: Each customer gets a separate DuploCloud Infrastructure.
* **Use Case**: Provides a higher security boundary at the network layer where customer access and data are separated.
* **Infrastructure**:
  * Separate VPC and network resources for each customer.
  * Clusters are inherently separate through Tenants isolated in different Infrastructures.
  * Higher cost due to duplicated resources and operational overhead.

### Cloud account per customer

<figure><img src="../.gitbook/assets/4 - Cloud Account.png" alt=""><figcaption><p>DuploCloud siloed account isolation and tenant per customer</p></figcaption></figure>

* **Description**: Each customer gets a separate cloud account.
* **Use Case**: The least common model, used for customers requiring complete isolation.
* **Infrastructure**:
  * Separate accounts with a DuploCloud platform installed in each.
  * Each account then has its own DuploCloud Infrastructure and Tenant.

### Hybrid model

<figure><img src="../.gitbook/assets/5 - Hybrid Tenancy Model (1).png" alt=""><figcaption><p>A hybrid of DuploCloud pooled tenancy model and shared cluster with separate namespace per tenant</p></figcaption></figure>

* **Description**: Combination of the above models as needed to meet specific requirements.
* **Use Case**: Diverse customer needs.
* **Infrastructure**:
  * A combination of previous models.
  * Organization-specific depending on requirements: some organizations may be in a pooled application environment whereas others may be more isolated through Tenant boundaries.

### Special hybrid case: single-tenant deployment in external Kubernetes cluster

<figure><img src="../.gitbook/assets/5.1 - Hybrid Tenancy Model - External Cluster.png" alt=""><figcaption></figcaption></figure>

* **Description**: DuploCloud imports existing Kubernetes clusters from external environments.
* **Use Case**: A cluster and resources already exist, or customers require the application or services solution running inside their client's cloud account. Customers are comfortable creating their own Kubernetes environments.
* **Infrastructure**:
  * Customer's cloud account or on-premises cluster (EKS, AKS, GKE, Oracle, DOKS, etc.) in connection with a DuploCloud Infrastructure. This could be any Kubernetes cluster not created by DuploCloud.&#x20;
  * Manages both multi-tenant and single-tenant environments from the DuploCloud UI.

## Documentation and support

* **Documentation**: [DuploCloud documentation](https://docs.duplocloud.com/docs) is available to support the development of your DuploCloud tenancy model.&#x20;
* **Support:** [DuploCloud customer support](https://docs.duplocloud.com/docs/welcome-to-duplocloud/duplocloud-support-model) can assist you in designing your deployment model or creating and managing Kubernetes clusters.
* **Low-code**: Terraform scripts and CLI instructions are available for creating EKS, AKS, or GKE clusters.
* **Resources**:
  * [https://marketplace.duplocloud.com/dashboard/duplocloud-tenancy-models](https://marketplace.duplocloud.com/dashboard/duplocloud-tenancy-models)
