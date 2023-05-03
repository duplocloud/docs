---
description: >-
  Enable Elastic Container Service (ECS) for AWS when creating a DuploCloud
  Infrastructure
---

# ECS Initial Setup

Setting up an Infrastructure that uses ECS is similar to creating an [Infrastructure that uses EKS](../kubernetes-cluster/), except that during creation, instead of selecting **Enable EKS**, you select **Enable ECS Cluster**.&#x20;

<figure><img src="../../../.gitbook/assets/AWS_ECS.png" alt=""><figcaption><p><strong>Add Infrastructure</strong> page with <strong>Enable ECS Cluster</strong> selected</p></figcaption></figure>

For information about ECS Services, see the [Containers and Services](../../aws-services/containers.md) documentation.

## Enable Read Only Processing for an ECS cluster

1. In the DuploCloud Portal, navigate to Administrator -> System Settings.
2. Click the System Config tab.
3. Click Add. The Add Config pane displays.
4. From the Config Type list box, select Flags.
5.
