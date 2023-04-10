---
description: Network configuration and how it maps to infrastructures in DuploCloud
---

# Infrastructure and Plan (VPC and network configuration)

{% hint style="info" %}
DuploCloud automatically deploys [NAT gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) across availability zones (AZs) for all Infrastructures that you create with DuploCloud.
{% endhint %}

When you create a DuploCloud Infrastructure, you create an isolated environment that maps to a Kubernetes cluster.&#x20;

Create a DuploCloud Infrastructure in the DuploCloud Portal:

1. Select **Administrator** -> **Infrastructure** from the navigation menu.&#x20;
2. Click **Add**.
3. Define the Infrastructure by completing the fields on the **Add Infrastructure** form.&#x20;
4. Select **Enable EKS** to enable EKS for the Infrastructure.
5. Optionally, select **Advanced Options** to specify additional configurations (public and private subnets, for example).
6. Click **Create**. The Infrastructure is created and is listed on the **Infrastructure** page.

![Add Infrastructure form](<../../.gitbook/assets/image (15) (1) (1) (2) (1) (1) (1) (1).png>)

When you create the Infrastructure, DuploCloud creates the following components:

* VPC with 2 subnets (private, public) in each availability zone
* Required security groups
* NAT Gateway
* Internet Gateway
* Route tables
* [VPC peering](../aws-services/virtual-private-cloud-vpc-peering.md) with the master VPC, which is initially configured in DuploCloud

Creating the DuploCloud Infrastructure can take some time. After the Infrastructure is created, a plan (with the same Infrastructure name) is created and populated with the configuration of the Infrastructure. The Plan is used to create [Tenants](tenant-environment.md).

![DuploCloud Plan Details](https://duplocloud.com/wp-content/uploads/2021/11/infra-plan.png)

{% hint style="warning" %}
Up to one instance (0 or 1) of an EKS or ECS is supported for each DuploCloud Infrastructure.
{% endhint %}

Once the Infrastructure is created, a [Plan ](../../getting-started/application-focussed-interface/plan.md)(with the same Infrastructure name) is automatically created and populated with the Infrastructure configuration. The Plan is used to create [Tenants](tenant-environment.md).
