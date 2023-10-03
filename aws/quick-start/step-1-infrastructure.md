---
description: Creating the DuploCloud Infrastructure and a Plan
---

# Step 1:  Create Infrastructure and Plan

Each DuploCloud Infrastructure is a Virtual Private Cloud (VPC) network that resides in a region that can host Kubernetes clusters, EKS or ECS clusters, or a combination of these, depending on your public cloud provider.&#x20;

After you supply a few basic inputs DuploCloud creates an Infrastructure for you, within AWS and within DuploCloud, with a few clicks. Behind the scenes, DuploCloud does a lot with what little you supply — generating the VPC, Subnets, NAT Gateway, Routes, and [EKS ](https://docs.aws.amazon.com/eks/)or [ECS ](https://docs.aws.amazon.com/ecs/)cluster.

With the Infrastructure as your foundation, you can customize an extensible, versatile Platform Engineering development environment by adding Tenants, Hosts, Services, and more.

_Estimated time to complete Step 1: 40 minutes. Much of this time is consumed by DuploCloud's creation of the Infrastructure and enabling your EKS cluster with Kubernetes._

## Prerequisites

Before starting this tutorial:

* Learn more about DuploCloud [Infrastructure](../../getting-started/application-focussed-interface/infrastructure.md)s, [Plan](../../getting-started/application-focussed-interface/plan.md)s, and [Tenant](../../getting-started/application-focussed-interface/tenant.md)s.
* Reference the [Access Control](../../administrator-tools/access-control/) documentation to create User IDs with the **Administrator** role. To perform the tasks in this tutorial, you must have Administrator privileges.

## Creating a DuploCloud Infrastructure

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**. The **Infrastructure** page displays.
2. Click **Add**. The **Add Infrastructure** page displays.
3. From the table below, enter the values that correspond to the fields on the **Add Infrastructure** page. Accept all other default values for fields not specified.&#x20;
4. Select either **Enable EKS** or **Enable ECS Cluster** options. You will follow different paths in the tutorial for creating Services with [EKS](quick-start-eks-services/), [ECS](quick-start-ecs-services/), or [DuploCloud Docker](quick-start-duplocloud-docker-services/).
5. Click **Create** to create the Infrastructure. It may take up to half an hour to create the Infrastructure. While the Infrastructure is being created, a **Pending** status is displayed in the Infrastructure page **Status** column, often with additional information about what part of the Infrastructure DuploCloud is currently creating. When creation completes, a status of **Complete** displays.&#x20;

DuploCloud begins creating and configuring your Infrastructure and EKS/ECS clusters using Kubernetes.&#x20;

| Add Infrastructure page field | Value                      |
| ----------------------------- | -------------------------- |
| **Name**                      | `nonprod`                  |
| **Region**                    | _`YOUR_GEOGRAPHIC_REGION`_ |
| **VPC CIDR**                  | `10.221.0.0/16`            |
| **Subnet CIDR Bits**          | `24`                       |

<div align="left">

<figure><img src="../../.gitbook/assets/AWS_QS_1.png" alt=""><figcaption><p><strong>Add Infrastructure</strong> page<br></p></figcaption></figure>

</div>

{% hint style="info" %}
It may take up to forty-five (45) minutes for your Infrastructure to be created and Kubernetes (EKS/ECS) enablement to be complete. Use the **Kubernetes** card in the Infrastructure screen to monitor the status, which should display as **Enabled** when completed. You can also monitor progress by using the **Kubernetes** tab, as DuploCloud generates your **Cluster Name**, **Default VM Size**, **Server Endpoint**, and **Token**.&#x20;
{% endhint %}

## Verifying that a Plan exists for your Infrastructure

Every DuploCloud Infrastructure generates a Plan. Plans are sets of templates that are used to configure the [Tenants ](../../getting-started/application-focussed-interface/tenant.md)or workspaces, in your Infrastructure. You will set up Tenants in the next tutorial step.

Before proceeding, confirm that a Plan exists that corresponds to your newly created Infrastructure.

1. In the DuploCloud Portal, navigate to **Administrator** -> **Plans**. The **Plans** page displays.
2. Verify that a Plan exists with the name **NONPROD,** the name that you gave to the Infrastructure you created.

## Checking your work

You previously verified that your Infrastructure and Plan were created. Now verify that Kubernetes is enabled before proceeding to Create a Tenant.

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**. The **Infrastructure** page displays.
2. From the Name column, select the **NONPROD** Infrastructure.
3. Click the **EKS** or **ECS** tabs. When Kubernetes has been **Enabled** for EKS or ECS, details are listed in the respective tab. The Infrastructure page displays the **Enabled** status on the **Kubernetes** card for EKS clusters. For ECS, the **Cluster Name** is listed in the **ECS** tab.

<div align="left">

<figure><img src="../../.gitbook/assets/AWS_QS_2.png" alt=""><figcaption><p>DuploCloud Infrastructure <strong>NONPROD</strong> with <strong>EKS</strong> tab displaying details and <strong>EKS</strong> card displaying <strong>Enabled</strong> </p></figcaption></figure>

</div>



<div align="left">

<figure><img src="../../.gitbook/assets/ecs_3.png" alt=""><figcaption><p>DuploCloud Infrastructure <strong>NONPROD-ECS-TEST</strong> with <strong>Cluster Nam</strong>e displaying in the <strong>ECS</strong> tab</p></figcaption></figure>

</div>

