---
description: How Infrastructures and Plans work together to create a VPC
---

# Infrastructure and Plan

Infrastructures are abstractions that allow you to create a Virtual Private Cloud (VPC) instance in the DuploCloud Portal. When you create an Infrastructure, a Plan is automatically generated to supply the network configuration necessary for your Infrastructure to run.&#x20;

DuploCloud creates a VNET with a default subnet and a default Network Security Group (NSG). The creation of an Infrastructure takes about ten (10) minutes.&#x20;

## Creating an Infrastructure

When you create a DuploCloud Infrastructure, you create an isolated environment that maps to a Kubernetes cluster.&#x20;

In DuploCloud, an [Infrastructure](../../../getting-started/application-focussed-interface/infrastructure.md) maps one-to-one to a VPC in a specified region. It also maps to a [Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine) (GKE) cluster you use for container orchestration.&#x20;

When creating an Infrastructure, specify the number of availability zones, the region, VPC Classless Inter-Domain Routing (CIDR), and a subnet mask. DuploCloud creates two subnets in each availability zone, one private and one public, and sets up routes and a NAT gateway.&#x20;

Create a DuploCloud Infrastructure in the DuploCloud Portal:

1. Click **Administrator** -> **Infrastructure** from the navigation menu.&#x20;
2. Click **Add**.
3. Define the Infrastructure by completing the fields on the **Add Infrastructure** form.&#x20;
4. Click **Enable GKE** to enable GKE for the Infrastructure.
5. Click the **Cluster Mode** list box, and select either **GKE Standard** or **Autopilot**.
6. Optionally, select **Advanced Options** to specify additional configurations (public and private subnets, for example).
7. Click **Create**. The Infrastructure is created and is listed on the **Infrastructure** page.

{% hint style="warning" %}
Up to one (0 or 1) GKS instance is supported for each DuploCloud Infrastructure.
{% endhint %}

When you create the Infrastructure, DuploCloud creates the following components:

* VPC with 2 subnets (private, public) in each availability zone
* Required security groups
* NAT Gateway
* Internet Gateway
* Route tables
* [VPC peering](../../../aws/aws-services/virtual-private-cloud-vpc-peering.md) with the master VPC, which is initially configured in DuploCloud

## About Plans and Infrastructures

Once the Infrastructure is created, a [Plan ](../../../getting-started/application-focussed-interface/plan.md)(with the same Infrastructure name) is automatically created and populated with the Infrastructure configuration. The Plan is used to create [Tenants](../../../azure/use-cases/tenant-environment.md).

<div align="left">

<img src="../../../.gitbook/assets/GCP_Plan_Details (1).png" alt="DuploCloud Plan Details for Infrastructure">

</div>
