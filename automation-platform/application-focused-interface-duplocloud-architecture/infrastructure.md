---
description: A conceptual overview of DuploCloud Infrastructures
---

# Infrastructure

Infrastructures are abstractions that allow you to create a Virtual Private Cloud (VPC) instance in the DuploCloud Portal. When you create an Infrastructure, a [Plan](plan.md) (with the same Infrastructure name) is automatically created and populated with the Infrastructure configuration.&#x20;

For instructions to create an Infrastructure in the DuploCloud Portal, see:

* [AWS Infrastructure](../../overview/use-cases/creating-an-infrastructure-and-plan-for-aws/)
* [Azure Infrastructure](../../automation-platform/overview-2/use-cases/infrastructure-and-plan/)
* [GCP Infrastructure](../../automation-platform/overview-1/use-cases/creating-an-infrastructure-and-plan-for-gcp/)
* [On-premises Infrastructure](../../automation-platform/kubernetes-overview/import-an-external-kubernetes-cluster.md#importing-your-kubernetes-cluster-to-duplocloud)

Each Infrastructure represents a network connection to a unique VPC/VNET, in a region with a Kubernetes cluster. For AWS, it can also include an ECS. An Infrastructure can be created with four basic inputs: Name, VPC CIDR, Number of AZs, Region, and a choice to enable or disable a K8S/ECS cluster. &#x20;

![The Add Infrastructure page in the DuploCloud Portal](<../../.gitbook/assets/image (69).png>)

When you create an Infrastructure, DuploCloud automatically creates the following components:

* VPC with two subnets (private, public) in each availability zone
* Required security groups
* NAT Gateway
* Internet Gateway
* Route tables
* [VPC peering](../../automation-platform/overview/aws-services/virtual-private-cloud-vpc-peering.md) with the master VPC, which is initially configured in DuploCloud

Additional requirements like custom Private/Public Subnet CIDRs can be configured in the **Advanced Options** area.&#x20;

{% hint style="info" %}
A common use case is two Infrastructures: one for Prod and one for Nonprod. Another is having an Infrastructure in a different region for disaster recovery or localized client deployments.
{% endhint %}

## Plans and Infrastructures

Once an Infrastructure is created, DuploCloud automatically creates a [Plan ](plan.md)(with the same Infrastructure name) with the Infrastructure configuration. The Plan is used to create [Tenants](../../automation-platform/overview/use-cases/tenant-environment/).

<figure><img src="../../.gitbook/assets/image (12) (2).png" alt=""><figcaption><p>The <strong>Plan Details</strong> pane in the DuploCloud Portal</p></figcaption></figure>
