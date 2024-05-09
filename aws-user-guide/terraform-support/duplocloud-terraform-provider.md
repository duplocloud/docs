# DuploCloud Terraform Provider

The DuploCloud provider offers a suite of resources for interacting with the DuploCloud API, facilitating the management of cloud infrastructure with ease. For comprehensive guidance and reference, the official documentation is available at:

[https://registry.terraform.io/providers/duplocloud/duplocloud/latest/docs](https://registry.terraform.io/providers/duplocloud/duplocloud/latest/docs)

## Retrieving EKS Cluster Names

In environments managed through DuploCloud, identifying the name of an Amazon EKS cluster via Terraform involves leveraging a data resource. This process is essential for operations that require the EKS cluster name, such as configuring Kubernetes resources or setting up IAM policies for cluster access.

To accurately obtain the EKS cluster name, follow these steps:

1. **Define a Data Resource**: Initiate a data resource in your Terraform configuration to pinpoint the DuploCloud infrastructure. This is contingent upon the `tenant_id` that your Terraform is applied to, as shown below:

    ```hcl
    data "duplocloud_infrastructure" "this" {
      tenant_id = local.tenant_id
    }
    ```

2. **Extract the Cluster Name**: The EKS cluster name is derived from the infrastructure name but prefixed with "duploinfra". This name can be stored in a Terraform local variable for easy reference throughout your configuration:

    ```hcl
    locals {
      eks_cluster_name = "duploinfra-${data.duplocloud_infrastructure.this.infra_name}"
    }
    ```

By integrating these steps into your Terraform scripts, you can seamlessly retrieve the name of your EKS cluster within a DuploCloud environment, ensuring your configurations are accurately targeted and effectively managed.