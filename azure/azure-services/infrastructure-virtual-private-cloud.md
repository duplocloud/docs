---
description: Create a DuploCloud infrastructure for Azure
---

# Infrastructure (Virtual Private Cloud)

When you create a DuploCloud Infrastructure, you create an isolated environment that maps to a Kubernetes cluster.&#x20;

Create a DuploCloud Infrastructure in the DuploCloud Portal:

1. Select **Administrator** -> **Infrastructure** from the navigation menu.&#x20;
2. Click **Add**. The **Add Infrastructure page** displays.
3. Define the Infrastructure by completing the fields on the **Add Infrastructure** page.&#x20;
4. Click **Create**. The Infrastructure is created and is listed on the **Infrastructure** page.

<figure><img src="../../.gitbook/assets/Azure_infra_default (2).png" alt=""><figcaption><p>Azure <strong>Infrastructure</strong> page</p></figcaption></figure>

When you create the Infrastructure, DuploCloud creates the following components:

* VPC with 2 subnets (private, public) in each availability zone
* Required security groups
* NAT Gateway
* Internet Gateway
* Route tables

Creating the DuploCloud Infrastructure can take some time. After the Infrastructure is created, a plan (with the same Infrastructure name) is created and populated with the configuration of the Infrastructure. The Plan is used to create [Tenants](../../aws/use-cases/tenant-environment.md).
