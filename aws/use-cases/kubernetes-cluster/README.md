---
description: >-
  Enable Elastic Kubernetes Service (EKS) for AWS by creating a DuploCloud
  Infrastructure
---

# EKS Initial Setup

In the DuploCloud platform, a Kubernetes Cluster maps to a DuploCloud Infrastructure.&#x20;

Start by creating a new Infrastructure in DuploCloud. When prompted to provide details for the new Infrastructure, select **Enable EKS**. In the **EKS Version** field, select the desired release.

The worker nodes and remaining workload setup is described in the [Tenant](../tenant-environment.md) topic.

![Add Infrastructure form with Enable EKS selected ](<../../../.gitbook/assets/image (15) (1) (1) (2) (1).png>)

{% hint style="info" %}
Creating an Infrastructure with EKS can take some time. See the Infrastructure section for details about other elements on the Add Infrastructure form.
{% endhint %}

{% hint style="warning" %}
Up to one instance (0 or 1) of an EKS or Elastic Container Service (ECS) is supported for each DuploCloud Infrastructure. &#x20;
{% endhint %}

When the Infrastructure is in the ready state, as indicated by a **Status** of **Complete**, select the **Name** of the Infrastructure page to view the Kubernetes configuration details, including the token and configuration for `kubectl`.&#x20;

<figure><img src="../../../.gitbook/assets/Infrastructure_Complete_AWS.png" alt=""><figcaption><p><strong>Infrastructure</strong> page with <strong>Status Complete</strong> displayed</p></figcaption></figure>

When you create Tenants in an Infrastructure, a namespace is created in the Kubernetes cluster with the name `duploservices-TENANT_NAME`
