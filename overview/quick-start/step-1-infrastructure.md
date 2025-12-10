---
description: Create a DuploCloud Infrastructure and Plan
---

# Step 1: Create Infrastructure and Plan

Each DuploCloud Infrastructure is a connection to a unique Virtual Private Cloud (VPC) network that resides in a region that can host Kubernetes clusters, EKS or ECS clusters, or a combination of these, depending on your public cloud provider.&#x20;

After you supply a few basic inputs, DuploCloud creates an Infrastructure within AWS and DuploCloud. Behind the scenes, DuploCloud does a lot with what little you supply, generating the VPC, subnets, NAT Gateway, routes, and [EKS ](https://docs.aws.amazon.com/eks/)or [ECS ](https://docs.aws.amazon.com/ecs/)clusters.

With the Infrastructure as your foundation, you can customize an extensible, versatile platform engineering development environment by adding Tenants, Hosts, Services, and more.

_Estimated time to complete Step 1: 40 minutes. Much of this time is consumed by DuploCloud's creation of the Infrastructure and enabling your EKS cluster with Kubernetes._

## Prerequisites

Before starting this tutorial:

* Learn more about DuploCloud [Infrastructures](../../introduction/application-focused-interface-duplocloud-architecture/infrastructure.md), [Plans](../../introduction/application-focused-interface-duplocloud-architecture/plan.md), and [Tenants](../../introduction/application-focused-interface-duplocloud-architecture/tenant.md).
* Reference the [Access Control](../../automation-platform/access-control/) documentation to create User IDs with the **Administrator** role. To perform the tasks in this tutorial, you must have Administrator privileges.

## Creating a DuploCloud Infrastructure

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**.
2. Click **Add**. The **Add Infrastructure** page displays.
3. Enter the values from the table below in the corresponding fields on the **Add Infrastructure** page. Accept default values for fields not specified.&#x20;
4. This tutorial offers different paths in the tutorial for creating Services with [EKS](../../automation-platform/overview/quick-start/quick-start-eks-services/), [ECS](../../automation-platform/overview/quick-start/quick-start-ecs-services/), or [DuploCloud Docker](../../automation-platform/overview/quick-start/quick-start-duplocloud-docker-services/). For creating ECS or EKS Services, select the following options:
   * **Enable ECS Cluster:** Choose this option to follow the ECS path in the tutorial.
   * **Enable EKS Cluster**, and set **Cluster Mode** to **Standard** to follow the EKS path.\
     If you prefer to use **Auto Mode**, which offers a fully managed EKS experience with no host access or custom AMIs, see the DuploCloud documentation for [EKS Auto Mode](../../automation-platform/overview/use-cases/eks-auto-mode.md).
5. Click **Create** to create the Infrastructure. It may take up to half an hour to create the Infrastructure. While the Infrastructure is being created, a **Pending** status is displayed in the Infrastructure page **Status** column, often with additional information about what part of the Infrastructure DuploCloud is currently creating. When creation completes, a status of **Complete** displays.&#x20;

| Add Infrastructure field    | Value                      |
| --------------------------- | -------------------------- |
| **Name**                    | `nonprod`                  |
| **Region**                  | _`YOUR_GEOGRAPHIC_REGION`_ |
| **VPC CIDR**                | `10.100.0.0/16`            |
| **Subnet CIDR Bits**        | `20`                       |
| **EKS Endpoint Visibility** | `Private`                  |

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot (663).png" alt=""><figcaption><p><strong>Add Infrastructure</strong> page<br></p></figcaption></figure></div>

{% hint style="info" %}
It may take up to forty-five (45) minutes for your Infrastructure to be created and Kubernetes (EKS/ECS) enablement to be complete. Use the **Kubernetes** card in the Infrastructure screen to monitor the status, which should display **Enabled** when complete. You can also monitor progress using the **Kubernetes** tab.
{% endhint %}

## Verifying That a Plan Exists for Your Infrastructure

Every DuploCloud Infrastructure generates a Plan. Plans are sets of templates that are used to configure the [Tenants ](../../introduction/application-focused-interface-duplocloud-architecture/tenant.md)or workspaces, in your Infrastructure. You will set up Tenants in the next tutorial step.

Before proceeding, confirm that a Plan exists that corresponds to your newly created Infrastructure.

1. In the DuploCloud Portal, navigate to **Administrator** -> **Plans**. The **Plans** page displays.
2. Verify that a Plan exists with the name **NONPROD**: the name of the Infrastructure you created.

## Checking Your Work <a href="#checking-your-work" id="checking-your-work"></a>

You previously verified that your Infrastructure and Plan were created. Now verify that Kubernetes is enabled before proceeding to create a Tenant.

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**. The **Infrastructure** page displays.
2. From the Name column, select the **NONPROD** Infrastructure.
3. Navigate to the **EKS** or **ECS** tab, depending on the platform you enabled.
4. Check Kubernetes status:
   * **For EKS:** Confirm that the **EKS** card on the right shows **Enabled**.
   * **For ECS:** Confirm that the **Cluster Name** appears in the **ECS** tab.

<figure><img src="https://docs.duplocloud.com/docs/~gitbook/image?url=https%3A%2F%2F2471407984-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F68cb0s9ce5UIUKWPuYs8%252Fuploads%252FxTgVbXY73FapIl00fHeu%252FScreenshot%2520%28171%29.png%3Falt%3Dmedia%26token%3Da3838c32-83b0-44fe-b103-836b14d1f2f1&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=da68430a&#x26;sv=2" alt=""><figcaption><p><strong>NONPROD</strong> Infrastructure page showing the EKS card with <strong>Enabled</strong>.</p></figcaption></figure>

<figure><img src="https://docs.duplocloud.com/docs/~gitbook/image?url=https%3A%2F%2F2471407984-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F68cb0s9ce5UIUKWPuYs8%252Fuploads%252F8vV6D7BEHcuFf9YXSwQi%252FScreenshot%2520%28172%29.png%3Falt%3Dmedia%26token%3Dbd455d12-ae1c-4677-b69f-83e79871baf3&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=16322e4c&#x26;sv=2" alt=""><figcaption><p><strong>NONPROD</strong> Infrastructure page with the Cluster Name displayed in the <strong>ECS</strong> tab.</p></figcaption></figure>
