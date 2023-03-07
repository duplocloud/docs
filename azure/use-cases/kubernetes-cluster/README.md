---
description: >-
  Enable Azure Managed Kubernetes Service (AKS) by creating a DuploCloud
  Infrastructure
---

# Infrastructure and AKS Setup

In the DuploCloud platform, a Kubernetes Cluster maps to a DuploCloud Infrastructure.&#x20;

Start by [creating a new Infrastructure in DuploCloud](disaster-recovery.md). The worker nodes and remaining workload setup is described in the [Tenant](../tenant-environment.md) topic.

![Add Infrastructure page ](../../../.gitbook/assets/Azure\_infra\_default.png)

{% hint style="info" %}
Creating an Infrastructure with AKS can take some time. See the [Infrastructure](disaster-recovery.md) section for details about other elements on the **Add Infrastructure** form.
{% endhint %}

{% hint style="warning" %}
Up to one instance (0 or 1) of an AKG is supported for each DuploCloud Infrastructure. &#x20;
{% endhint %}

When the Infrastructure is in the ready state, as indicated by a **Status** of **Complete**, select the **Name** of the Infrastructure to view the Kubernetes configuration details, including the token and configuration for `kubectl`.&#x20;

<figure><img src="../../../.gitbook/assets/Infrastructure_Complete_AWS.png" alt=""><figcaption><p><strong>Infrastructure</strong> page with <strong>Status Complete</strong> displayed</p></figcaption></figure>

## AKS Setup

After creating the Infrastructure and plan, you must [enable the Azure Kubernetes Service](../../quick-start/step-1-infrastructure.md#enabling-the-aks-kubernetes-cluster) to connect Azure with Kubernetes.
