---
description: Working with Load Balancers using AWS ECS
---

# ECS Services and Load Balancers

## Prerequisites

Before you create an ECS Service and Load Balancer, you must create a [Task Definition](../../../aws-user-guide/aws-services/containers/ecs-containers-and-task-definitions.md) to run the Service. You can define multiple containers in your Task Definition.

## Adding an ECS Service and Load Balancer Listener

{% hint style="info" %}
For an end-to-end example of deploying an application using an ECS Service, see the [AWS Quick Start Tutorial](../../quick-start/) and choose the [Creating an ECS Service](../../quick-start/quick-start-ecs-services/) option.
{% endhint %}

Tasks run until an error occurs or a user terminates the Task in the ECS Cluster.

1. Navigate to **Cloud Services** -> **ECS**.
2. In the **Task Definitions** tab, select the Task Definition Family Name. This is the [Task Definition **Name** that you created ](../../../aws-user-guide/aws-services/containers/ecs-containers-and-task-definitions.md)prepended by a unique DuploCloud identifier. &#x20;
3.  In the **Service Details** tab, click the **Configure ECS Service** link. The **Add ECS Service** page displays.\


    <figure><img src="../../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.19-14_27_18.png" alt=""><figcaption><p>Add ECS Service page</p></figcaption></figure>
4. In the **Name** field, enter the Service name.
5.  In the **LB Listeners** area, click **Add**. The **Add Load Balancer Listener** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/dockerq (1).png" alt="" width="311"><figcaption><p><strong>Add Load Balancer Listener</strong> pane for an ECS Service</p></figcaption></figure></div>


6. From the **Select Type** list box, select **Application LB**.
7. In the **Container Port** field, enter a container port number.
8. In the **External Port** field, enter an external port number.
9. From the **Visibility** list box, select an option.
10. In the **Heath Check** field, enter a path (such as **/**) to specify the location of Kubernetes Health Check logs.
11. From the **Backend Protocol** list box, select **HTTP**.
12. From the **Protocol Policy** list box, select **HTTP1**.
13. Select other options as needed and click **Add**.
14. On the **Add ECS Service** page, click **Submit**.&#x20;

Verify the Service and Load Balancer configuration details in the **Service Details** tab on the Task Definition details page.&#x20;

<figure><img src="../../../.gitbook/assets/ecs_8 (1).png" alt=""><figcaption><p><strong>Service Details</strong> tab displaying Service and Load Balancer configuration details</p></figcaption></figure>

## Additional Load Balancer Settings

You can use the **Other Settings** card in the DuploCloud Portal to set the following features:

* WAF Web ACL
* Enable HTTP to HTTPS redirects
* Enable Access Logging
* Set Idle Timeout
* Drop invalid headers
* Delete Protection

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **ECS**, and select the **Services** tab.
2. Select the Service to which your Load Balancer is attached from the **NAME** column.
3. Click the **Load Balancers** tab.
4.  In the **Other Settings** card, click **Edit**. \


    <figure><img src="../../../.gitbook/assets/other settings (2).png" alt=""><figcaption></figcaption></figure>
5. The **Other Load Balancer Settings** pane displays.

<div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (68).png" alt="" width="302"><figcaption><p>The <strong>Other Load Balancer Settings</strong> pane</p></figcaption></figure></div>

6. Configure the settings, as needed.
7. Click **Save**. The Load Balancer settings are updated.&#x20;
