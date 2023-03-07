---
description: Dynamically configure Azure agent pools for optimum performance
---

# Autoscaling Azure Agent Pools

When you use autoscaling for Azure agent pools, you allow DuploCloud to manage your application's capacity requirements within your limits.&#x20;

## Creating an autoscaled Azure agent pool

In the DuploCloud Portal, [create an Azure agent pool](../../azure-services/agent-pool.md) with the Enable Autoscaling option selected. Each agent pool contains nodes backed by the virtual host machines.

<figure><img src="../../../.gitbook/assets/Agent_Pool_Azure (1).png" alt=""><figcaption><p><strong>Azure Agent Pool</strong> page with <strong>Enable Autoscaling</strong> option</p></figcaption></figure>

## Configure Service with HPA

Configure a service with the [Kubernetes Horizontal Pod Autoscaler (HPA)](autoscaling-in-kubernetes.md#kubernetes-horizontal-pod-autoscaler-hpa) to manage autoscaling for the agent pool.
