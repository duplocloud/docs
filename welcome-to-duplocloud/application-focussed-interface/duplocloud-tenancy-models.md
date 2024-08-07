---
description: An outline of the tenancy deployment models supported by DuploCloud
---

# DuploCloud Tenancy Models

DuploCloud supports a variety of deployment models, from basic multi-tenant applications to complex single-Tenant deployments within customer environments. These models cater to different security needs, allowing customers to achieve their desired isolation level while maintaining operational efficiency.&#x20;

DuploCloud-supported tenancy models, outlined below, include:

* [Application-managed multi-tenancy](duplocloud-tenancy-models.md#application-managed-multi-tenancy)
* [DuploCloud Tenant-per-customer](duplocloud-tenancy-models.md#duplocloud-tenant-per-customer)
* [DuploCloud Infrastructure-per-customer](duplocloud-tenancy-models.md#duplocloud-infrastructure-per-customer)
* [Cloud account-per-customer](duplocloud-tenancy-models.md#cloud-account-per-customer)
* [Hybrid model](duplocloud-tenancy-models.md#hybrid-model)
* [On-premises ](duplocloud-tenancy-models.md#special-hybrid-case-single-tenant-deployment-in-external-kubernetes-cluster)

## Tenancy Deployment Models

### Application-Managed Multi Tenancy

<figure><img src="../../.gitbook/assets/1 - Application Provides Tenancy.png" alt=""><figcaption><p>DuploCloud pooled tenancy model</p></figcaption></figure>

* **Description**: The application manages tenant isolation with DuploCloud structured pooled tenancy.&#x20;
* **Use Case**: The most common scenario is where the application logic isolates customer data. DuploCloud Tenants are then used to isolate development environments (i.e., Nonprod and Prod).&#x20;
* **Infrastructure**:
  * Shared DuploCloud Infrastructure (VPC, Tenant, VM/instances, S3 bucket, RDS). Cluster/namespace can also be shared.&#x20;
  * Scaling: Increase compute instances for Kubernetes worker nodes as needed.

### DuploCloud Tenant-per-Customer

<figure><img src="../../.gitbook/assets/2 - DuploCloud Tenant.png" alt=""><figcaption><p>A visual representation of a DuploCloud shared cluster with separate namespace per tenant</p></figcaption></figure>

* **Description**: Each customer gets a separate DuploCloud Tenant.
* **Use Case**: Suitable for older applications not designed for multi-tenancy, or security and compliance needs.
* **Infrastructure**:
  * Shared network layer (VPC).
  * Separate Tenants per customer with security boundaries (security group, KMS key, SSH key, Kubernetes namespace).
  * Kubernetes cluster is shared and boundaries are through the namespace.

### DuploCloud Infrastructure-per-Customer

<figure><img src="../../.gitbook/assets/3 - DuploCloud Infrastructure.png" alt=""><figcaption><p>A visual representation of a DuploCloud siloed cluster per Tenant with separate network infrastructure</p></figcaption></figure>

* **Description**: Each customer gets a separate DuploCloud Infrastructure.
* **Use Case**: Provides a higher security boundary at the network layer where customer access and data are separated.
* **Infrastructure**:
  * Separate VPC and network resources for each customer.
  * Clusters are inherently separate through Tenants isolated in different Infrastructures.
  * Higher cost due to duplicated resources and operational overhead.

### Cloud Account-per-Customer

<figure><img src="../../.gitbook/assets/4 - Cloud Account.png" alt=""><figcaption><p>A visual representation of a DuploCloud siloed account isolation and Tenant-per-customer</p></figcaption></figure>

* **Description**: Each customer gets a separate cloud account.
* **Use Case**: The least common model, used for customers requiring complete isolation.
* **Infrastructure**:
  * Separate accounts with a DuploCloud Platform installed in each.
  * Each account then has its own DuploCloud Infrastructure and Tenant.

### Hybrid Model

<figure><img src="../../.gitbook/assets/5 - Hybrid Tenancy Model (1).png" alt=""><figcaption><p>A visual representation of a hybrid of DuploCloud pooled tenancy model and shared cluster with a separate namespace-per-Tenant</p></figcaption></figure>

* **Description**: Combination of the above models as needed to meet specific requirements.
* **Use Case**: Diverse customer needs.
* **Infrastructure**:
  * A combination of previous models.
  * Organization-specific depending on requirements: some organizations may be in a pooled application environment whereas others may be more isolated through Tenant boundaries.

### Special Hybrid Case: Single-Tenant Deployment in an External Kubernetes Cluster

<figure><img src="../../.gitbook/assets/5.1 - Hybrid Tenancy Model - External Cluster.png" alt=""><figcaption></figcaption></figure>

* **Description**: DuploCloud imports existing Kubernetes clusters from external environments.
* **Use Case**: A cluster and resources already exist, or customers require the application or services solution running inside their client's cloud account. Customers are comfortable creating their own Kubernetes environments.
* **Infrastructure**:
  * Customer's cloud account or On-premises cluster (EKS, AKS, GKE, Oracle, DOKS, etc.) in conjunction with a DuploCloud Infrastructure. This could be any Kubernetes cluster not created by DuploCloud.&#x20;
  * Manages both multi-Tenant and single-Tenant environments from the DuploCloud UI.

## Documentation and Support

* **Documentation**: [DuploCloud documentation](https://docs.duplocloud.com/docs) is available to support the development of your DuploCloud tenancy model.&#x20;
* **Support:** [DuploCloud customer support](https://docs.duplocloud.com/docs/welcome-to-duplocloud/duplocloud-support-model) can assist you in designing your deployment model or creating and managing Kubernetes clusters.
