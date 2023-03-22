---
description: Network configuration and how it maps to infrastructures in DuploCloud
---

# Networks and DuploCloud infrastructures

{% hint style="info" %}
DuploCloud automatically deploys Cloud NAT Gateways across availability zones (AZs) for all Infrastructures that you create with DuploCloud GCP.
{% endhint %}

Networking is a foundational piece of the DevOps lifecycle and the first thing you must configure when using DuploCloud. Key networking concepts include:

* Virtual Private Cloud (VPC)
* Subnets
* Region
* Availability zones (AZs)
* Network Address Translation (NAT) gateway
* Routing

In DuploCloud, an Infrastructure maps one-to-one to a VPC in a specified region. It also maps to a cluster that you use for container orchestration.&#x20;

When creating an Infrastructure, you specify the number of availability zones, the region, VPC Classless Inter-Domain Routing (CIDR), and a subnet mask. DuploCloud creates two subnets in each availability zone, one private and one public, and sets up routes and a NAT gateway.&#x20;

![Add Infrastructure form](../../.gitbook/assets/GCP\_Infra\_Add.png)

See the [Infrastructure](../gcp-services/infrastructure-virtual-private-cloud.md) topic for detailed steps about how to create an Infrastructure in the DuploCloud Portal.

{% hint style="warning" %}
Up to one instance (0 or 1) of a GKE, EKS/Native, or ECS is supported for each DuploCloud Infrastructure.
{% endhint %}

Once the Infrastructure is created, a [Plan](../../getting-started/application-focussed-interface/plan.md) (with the same Infrastructure name) is automatically created and populated with the Infrastructure configuration. The Plan is used to create [Tenants](../../getting-started/application-focussed-interface/tenant.md).

![DuploCloud Plan Details](../../.gitbook/assets/GCP\_Plan\_Details.png)
