---
description: Create a DuploCloud infrastructure for AWS.
---

# Infrastructure (Virtual Private Cloud)

When you create a DuploCloud Infrastructure, you create an isolated environment that maps to a Kubernetes cluster.&#x20;

Create a DuploCloud Infrastructure in the DuploCloud Portal:

1. Select **Administrator** -> **Infrastructure** from the navigation menu.&#x20;
2. Click **Add**.
3. Define the Infrastructure by completing the fields on the **Add Infrastructure** form.&#x20;
4. Select **Enable EKS** to enable EKS for the Infrastructure.
5. Optionally, select **Advanced Options** to specify additional configurations (public and private subnets, for example).
6. Click **Create**. The Infrastructure is created and is listed on the **Infrastructure** page.

&#x20; &#x20;

![Add Infrastructure form](https://duplocloud.com/wp-content/uploads/2021/11/create-infra.png)

When you create the Infrastructure, DuploCloud creates the following components:

* VPC with 2 subnets (private, public) in each availability zone
* Required security groups
* NAT Gateway
* Internet Gateway
* Route tables
* [VPC peering](virtual-private-cloud-vpc-peering.md) with the master VPC, which is initially configured in DuploCloud

Creating the DuploCloud Infrastructure can take some time. After the Infrastructure is created, a plan (with the same Infrastructure name) is created and populated with the configuration of the Infrastructure. The Plan is used to create [Tenants](../../use-cases/tenant-environment.md).

![DuploCloud Plan Details](https://duplocloud.com/wp-content/uploads/2021/11/infra-plan.png)
