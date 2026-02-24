---
description: Share EC2 Auto Scaling Groups Across Tenants for ECS
---

# Sharing EC2 Auto Scaling Groups Across Tenants for ECS

DuploCloud supports sharing EC2 Auto Scaling Groups (ASGs) across Tenants for ECS services. This allows multiple Tenants to consume a common pool of ECS hosts, improving host utilization and centralizing infrastructure management. Tenant isolation is preserved, as each Tenant can only view and manage its own ECS tasks, even when those tasks are running on shared hosts.

## Configuring EC2 ASG Sharing for ECS Services&#x20;

### Enabling Host Sharing Tenant Settings

To allow ECS tasks to run on Hosts from another Tenant, both Tenants must have the correct settings enabled:

1. Navigate to **Administrator** → **Tenants**.
2. Select the Tenant in the **NAME** column.
3. Select the **Settings** tab.
4. Click **Add**. The **Add Tenant Feature** pane displays.
5. In the **Select Feature** list box, select the appropriate setting for the Tenant:
   * Tenant running hosts: **Allow hosts to run K8S pods/ECS Task from other tenants**
   * Tenant(s) running tasks: **Enable option to run K8S pods/ECS Task on any host**<br>

{% columns %}
{% column width="50%" %}
<figure><img src="../../../../../.gitbook/assets/image (480).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column width="50%" %}
<figure><img src="../../../../../.gitbook/assets/image (481).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

6. Select **Enable**, and click **Add** to save.

### Creating a Shared ASG

In the Tenant that you want to run the hosts:

1. [Create an ASG](../../../use-cases/hosts-vms/auto-scaling/auto-scaling-groups/#creating-autoscaling-groups-asg).
   * Select **ECS** in the **Agent Platform** field.
2. Wait until at least one EC2 host is running and registered with ECS before using it.

### Using a Shared ASG in ECS Services

In the Tenant that you want to run ECS tasks:

1. [Create an ECS Task Definition](../../../../../overview/aws-services/containers/ecs-containers-and-task-definitions/#creating-a-task-definition).&#x20;
   * In the **Launch Type** field, select **EC2**.
2. Using this task definition, [create an ECS Service](../../../../../overview/aws-services/containers/ecs-containers-and-task-definitions/#creating-an-ecs-service).&#x20;
   * Select the shared ASG from the **Capacity Provider** list box.

{% hint style="info" %}
The shared ASG only appears in the Capacity Provider list box if the following conditions are met:

* **Host sharing settings are enabled** in both Tenants.
* **At least one ECS Linux Host** is running in the provider ASG.
* The **launch type is EC2** (shared ASGs are not supported for Fargate tasks).
{% endhint %}
