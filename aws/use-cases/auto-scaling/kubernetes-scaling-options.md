---
description: Autoscale your DuploCloud Kubernetes deployment
---

# Autoscaling in Kubernetes

## Prerequisites

Before autoscaling can be configured for your Kubernetes service, make sure that:

1. [Autoscaling Group (ASG)](auto-scaling-groups.md) is setup in the DuploCloud tenant
2. [Cluster Autoscaler](../disaster-recovery/kubernetes-cluster/enable-cluster-autoscaler.md) is enabled for your DuploCloud infrastructure

## Kubernetes Horizontal Pod Autoscaler (HPA)

Horizontal Pod Autoscaler (HPA) automatically scales the Deployment and its ReplicaSet. HPA checks the metrics configured in regular intervals and then scales the replicas up or down accordingly.

### Configuring Services with HPA

You can configure HPA while creating a Deployment Service from the DuploCloud Portal.

1. In the DuploCloud Portal, navigate **DevOps** > **Containers** > **EKS/Native.**
2. In the **Service** tab, create a new [Service](../../aws-services/containers/) by clicking **Add**.
3.  In **Add Service - Basic Options**, from the **Replication Strategy** list box, select **Horizontal Pod Scheduler**_._ \


    <div align="left">

    <img src="../../../.gitbook/assets/hpa1.png" alt="Basic Options on the Add Service page, with Replication Strategy list box and Horizontal Pod Autoscaler Config fields">

    </div>


4.  In the **Horizontal Pod Autoscaler Config** field, add a sample configuration, as shown below. Update the minimum/maximum Replica Count in the `resource` attributes, based on your requirements. \


    <div align="left">

    <figure><img src="../../../.gitbook/assets/hpa_Code_block.png" alt=""><figcaption><p><strong>Horizontal Pod Autoscaler Config</strong> field in <strong>Basic Options</strong>, on the <strong>Add Service</strong> page</p></figcaption></figure>

    </div>


5. Click **Next** to navigate to **Advanced Options**.
6.  In **Advanced Options**, in the **Other Container Config** field, ensure your resource attributes, such as `Limits` and `Requests`, are set to work with your HPA configuration, as in the example below.\


    <div align="left">

    <img src="../../../.gitbook/assets/Screen Shot 2022-07-16 at 12.02.11 PM.png" alt="Other Container Config field in Advanced Options on the Add Service page">

    </div>
7. At the bottom of the **Advanced Options** page, click **Create**.

{% hint style="info" %}
For HPA Configures Services, **Replica** is set as _Auto_ in the DuploCloud Portal
{% endhint %}

When your services are running, **Replicas: Auto** is displayed on the Service page.

<div align="left">

<img src="../../../.gitbook/assets/image (8) (3).png" alt="Service page with Replicas: Auto and Status: Running displayed">

</div>

