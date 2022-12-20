---
description: Dynamically configure Azure agent pools for optimum performance
---

# Autoscale agent pools

When you use autoscaling for Azure agent pools, you allow DuploCloud to manage your application's capacity requirements within your limits. To enable autoscaling, you:

1. Create an Azure agent pool with autoscaling enabled.
2. Configure a service using Kubernetes Horizontal Pod Autoscaling (HPA) to manage autoscaling.

### Step 1: Create an autoscaled Azure agent pool

In the DuploCloud Portal, [create an Azure agent pool](../azure-services/agent-pool.md) with the **Enable Autoscaling** option selected. Each agent pool contains nodes backed by the virtual host machines.

![Input fields on the Add Azure Agent Pool page with Enable Autoscaling selected.](<../../.gitbook/assets/image (59).png>)

### Step 2: Configure Service with HPA

Configure a service with the [Kubernetes Horizontal Pod Autoscaler (HPA)](../../aws/use-cases/auto-scaling/kubernetes-scaling-options.md#kubernetes-horizontal-pod-autoscaler-hpa) to manage autoscaling for the agent pool.&#x20;
