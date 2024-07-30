# Infrastructure

Infrastructures are abstractions that allow you to create a Virtual Private Cloud (VPC) instance in the DuploCloud Portal. When you create an Infrastructure, a [Plan](plan.md) (with the same Infrastructure name) is automatically created and populated with the Infrastructure configuration to supply the network configuration necessary for your Infrastructure to run.&#x20;

For instructions to create an Infrastructure in the DuploCloud Portal, see:

* [AWS Infrastructure](../../../overview/use-cases/creating-an-infrastructure-and-plan-for-aws/)
* [Azure Infrastructure](../../../overview-2/use-cases/infrastructure-and-plan/)
* [GCP Infrastructure](../../../overview-1/use-cases/creating-an-infrastructure-and-plan-for-gcp/)
* [On-Premises Infrastructure](../../../extras-overview/import-an-external-kubernetes-cluster.md#importing-your-kubernetes-cluster-to-duplocloud)

Each Infrastructure represents a network connection to a unique VPC/VNET, in a region with a Kubernetes cluster. In the case of AWS, it can also include an ECS. An Infrastructure can be created with four basic inputs: Name, VPC CIDR, Number of AZs, Region, and the option to enable or disable a K8S/ECS cluster. &#x20;

![Infrastructure Creation Screen](<../../../.gitbook/assets/image (12) (4).png>)

When you create the Infrastructure, DuploCloud automatically creates the following components:

* VPC with two subnets (private, public) in each availability zone
* Required security groups
* NAT Gateway
* Internet Gateway
* Route tables
* [VPC peering](../../../overview/aws-services/virtual-private-cloud-vpc-peering.md) with the master VPC, which is initially configured in DuploCloud

Additional requirements like custom Private/Public Subnet CIDRs can be configured in the Advanced Options area.&#x20;

{% hint style="info" %}
A common use for Infrastructure is having two Infrastructures, one for prod and one for non-prod. Another is having an infrastructure in a different region for DR or localized client deployments in that region.
{% endhint %}

## Plans and Infrastructures

Once the Infrastructure is created, DuploCloud automatically creates a [Plan ](plan.md)(with the same Infrastructure name) with the Infrastructure configuration. The Plan is used to create [Tenants](../../../overview/use-cases/tenant-environment/).

<figure><img src="../../../.gitbook/assets/image (157).png" alt=""><figcaption></figcaption></figure>
