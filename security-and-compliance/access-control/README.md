# Isolation and Firewall

Isolation of concerns and environments is the most basic principle in any infrastructure security implementation. The cloud providers allow many constructs to implement this isolation to varying degrees. As an example one can isolate two workloads in completely different "cloud accounts", or different "VPCs" within the same account or different "security groups" within the same VPC. Then there are other constructs like IAM (AWS Roles, Azure managed Identity, GCP service accounts) or Kubernetes namespace and so forth. A big challenge is how do we bring together dozens of these security constructs and map them to an application centric isolation model.&#x20;

DuploCloud brings these constructs together in an application centric model shown in the following picture which is described in more detail in the previous section [here](../../getting-started/application-focussed-interface/). To summarize it, we have 3 layers if isolation:

* **Account Level**: This is the heaviest hammer and the deepest grade of separation. Being heavy weight it also incurs maximum overhead in terms of maintenance and cost as almost no construct can be reused across two environments.&#x20;
* **VPC Level (a.k.a **_**DuploCloud Infrastructure**_**)**: Within the same account, environments are segregated by virtual networks (VPC/ VNET).
* **Security group and IAM (a.k.a **_**DuploCloud Tenant**_**)**: Within the same account and same VPC, we can isolate by having separate security groups, IAM roles (Managed Identity in AWS, Service accounts in GCP) , encryption keys etc. Tenant is like an environment. Two tenants can be in the same VPC, different VPC or in different VPCs in different accounts.

{% hint style="info" %}
**Tenant is like a Kubernetes namespace but at an extended cloud provider scope**. Most cloud resources directly consumed by applications are within a tenant like databases, queues, storage, VMs etc. Some resources are of course shared as well like VPC, VMs, Encryption Keys, SSL certs etc. One can also create resources in one tenant and allow others to consume those via inter-tenant access policies.  &#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

&#x20; &#x20;
