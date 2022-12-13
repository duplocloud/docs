# Networking

Networking is the most foundational piece in the Devops lifecycle and setup the very beginning. The key concepts involved are

* VPC
* Subnets
* Region
* Availability zones
* NAT Gateway
* Routing

In DuploCloud the concept of [Infrastructure](../../getting-started/application-focussed-interface/infrastructure.md) maps one-to-one to a VPC in a specified region. While creating Infrastructure the user can specify the count of availability zones, region, VPC CIDR and a Subnet Mask. Internally the platform will create 2 subnets in each AZ (one private and one public), setup up routes and NAT gateway.&#x20;

![](<../../.gitbook/assets/image (15) (1) (1) (2) (1) (1).png>)

Infrastructure also maps to a Kubernetes or ECS Cluster. This is optional if the user wants to use Kubernetes or ECS for container orchestration

{% hint style="warning" %}
At this moment per infrastructure only one EKS or ECS cluster is supported. One can have both EKS as well as ECS cluster but only 1 or 0 of each.&#x20;
{% endhint %}



Once the infrastructure complete, a new [Plan](../../getting-started/application-focussed-interface/plan.md) with the same infrastructure name is automatically created and populated with the details of the newly created infrastructure. This plan can then be used to create the [Tenants](../../getting-started/application-focussed-interface/tenant.md).

![](https://duplocloud.com/wp-content/uploads/2021/11/infra-plan.png)
