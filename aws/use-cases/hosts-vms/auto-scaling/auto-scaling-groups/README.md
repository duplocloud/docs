---
description: Create Autoscaling groups to scale EC2 instances to your workload
---

# Autoscaling Groups (ASG)

Configure Autoscaling Groups (ASG) to ensure the application load is scaled based on the number of EC2 instances configured. Autoscaling detects unhealthy instances and launches new EC2 instances. ASG is also cost-effective as EC2 Instances are dynamically created as per the application requirement within minimum and maximum count limits.&#x20;

## Creating Autoscaling Groups (ASG)

{% hint style="info" %}
The Use for Cluster Autoscaling option will not be available until you enable the [Cluster Autoscaler option in your Infrastructure](./#configuring-cluster-autoscaler-for-your-infrastructure).
{% endhint %}

1. In the DuploCloud Portal, navigate to **DevOps** -> **Hosts**.
2. In the **ASG** tab, click **Add**. The **Add ASG** page is displayed.
3. Select **Use for Cluster Autoscaling**.
4. In the **Friendly Name** field, enter the name of the ASG.
5. In the **Instance Count** field, enter the desired capacity for the Autoscaling group.
6. In the **Minimum Instances** field, enter the minimum number of instances. The Autoscaling group ensures that the total number of instances is always greater than or equal to the minimum number of instances.
7. In the **Maximum Instances** field, enter the maximum number of instances. The Autoscaling group ensures that the total number of instances is always less than or equal to the maximum number of instances.
8. From the **Platform** list box, select **Linux Docker/Native** to run a Docker service or select **EKS Linux** to run services using EKS.
9.  Optionally, enable [Spot Instances](spot-instances.md#enabling-spot-instances-when-creating-autoscaling-groups).\


    ![Add ASG page with Use for Cluster Autoscaling option selected](<../../../../../.gitbook/assets/image (22) (1).png>)
10. Click **Add**. Your ASG is added and displayed in the **ASG** tab.

## Viewing Hosts in Autoscaling Groups

View the Hosts created as part of ASG creation from ASG View Details Page.

![Hosts tab on the ASG page](<../../../../../.gitbook/assets/image (11) (1).png>)

## **Creating an Amazon EC2 Autoscaling Policy**

Refer to AWS [Documentation](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scale-based-on-demand.html#as-how-scaling-policies-work) for detailed steps on creating Scaling policies for the Autoscaling Group created

## **Creating Services using Autoscaling Groups**

The DuploCloud Portal provides the ability to configure Services based on the platforms **EKS Linux** and **Linux Docker/Native**.  Select the ASG based on the platform used when creating services and Autoscaling groups. Optionally, if you previously [enabled Spot Instances in the ASG](spot-instances.md#enabling-spot-instances-when-creating-autoscaling-groups), you can configure the Service to use Spot Instances by selecting **Tolerate spot instances**.&#x20;

![ASG name with EKS Linux](<../../../../../.gitbook/assets/image (17) (1).png>)

![ASG name using Linux Docker/Native](<../../../../../.gitbook/assets/image (13) (1).png>)
