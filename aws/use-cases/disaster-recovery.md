---
description: How Infrastructures and Plans work together to create a VPC
---

# Infrastructure (VPC) and Plan (configuration)

Infrastructures are abstractions that allow you to create a Virtual Private Cloud (VPC) instance in the DuploCloud Portal. When you create an Infrastructure, a Plan is automatically generated to supply the network configuration necessary for your Infrastructure to run.&#x20;

{% hint style="info" %}
DuploCloud automatically deploys [NAT gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) across availability zones (AZs) for all Infrastructures that you create with DuploCloud.
{% endhint %}

## Creating an Infrastructure

When you create a DuploCloud Infrastructure, you create an isolated environment that maps to a Kubernetes cluster.&#x20;

Create a DuploCloud Infrastructure in the DuploCloud Portal:

1. Select **Administrator** -> **Infrastructure** from the navigation menu.&#x20;
2. Click **Add**.
3. Define the Infrastructure by completing the fields on the **Add Infrastructure** form.&#x20;
4. Select **Enable EKS** to enable EKS for the Infrastructure.
5. Optionally, select **Advanced Options** to specify additional configurations (such as [**Public** and **Private CIDR** Endpoints](disaster-recovery/kubernetes-cluster/enable-eks-endpoints.md)).
6. Click **Create**. The Infrastructure is created and is listed on the **Infrastructure** page.

![AWS Add Infrastructure form](<../../.gitbook/assets/image (15) (1) (1) (2) (1) (1) (1) (1).png>)

When you create the Infrastructure, DuploCloud creates the following components:

* VPC with 2 subnets (private, public) in each availability zone
* Required security groups
* NAT Gateway
* Internet Gateway
* Route tables
* [VPC peering](../aws-services/virtual-private-cloud-vpc-peering.md) with the master VPC, which is initially configured in DuploCloud

## About Plans and Infrastructures

Once the Infrastructure is created, DuploCloud automatically creates a [Plan ](../../getting-started/application-focussed-interface/plan.md)(with the same Infrastructure name) with the Infrastructure configuration. The Plan is used to create [Tenants](tenant-environment.md).

![DuploCloud Plan Details](https://duplocloud.com/wp-content/uploads/2021/11/infra-plan.png)

{% hint style="warning" %}
Up to one instance (0 or 1) of an EKS or ECS is supported for each DuploCloud Infrastructure.
{% endhint %}
