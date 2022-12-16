---
description: Network configuration and how it maps to infrastructures in DuploCloud
---

# Networks and DuploCloud infrastructures

Networking is a foundational piece of the DevOps lifecycle and the first thing you must configure when using DuploCloud. Key networking concepts include:

* Virtual Private Cloud (VPC)
* Subnets
* Region
* Availability zones (AZs)
* Network Address Translation (NAT) gateway
* Routing

In DuploCloud, an [Infrastructure](../../getting-started/application-focussed-interface/infrastructure.md) maps one-to-one to a VPC in a specified region. It also maps to an Elastic Kubernetes Service (EKS) or Elastic Container Service (ECS) cluster that you use for container orchestration.&#x20;

When creating an Infrastructure, you specify the number of availability zones, the region, VPC Classless Inter-Domain Routing (CIDR), and a subnet mask. DuploCloud creates two subnets in each availability zone, one private and one public, and sets up routes and a NAT gateway.&#x20;

![Add Infrastructure form](<../../.gitbook/assets/image (15) (1) (1) (2) (1) (1).png>)

See the [Infrastructure](../aws-services/infrastructure.md) topic for detailed steps about how to create an Infrastructure in the DuploCloud Portal.

{% hint style="warning" %}
Up to one instance (0 or 1) of an EKS or ECS is supported for each DuploCloud Infrastructure.
{% endhint %}

Once the Infrastructure is created, a [Plan ](../../getting-started/application-focussed-interface/plan.md)(with the same Infrastructure name) is automatically created and populated with the Infrastructure configuration. The Plan is used to create [Tenants](tenant-environment.md).

![DuploCloud Plan Details](https://duplocloud.com/wp-content/uploads/2021/11/infra-plan.png)
