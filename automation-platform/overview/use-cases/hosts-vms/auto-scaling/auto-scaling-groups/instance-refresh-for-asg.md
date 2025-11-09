---
description: >-
  Initiate an Instance Refresh for an Auto Scaling Group (ASG) within the
  DuploCloud Portal.
---

# Instance Refresh for ASG

Instance refresh allows you to apply configuration changes to existing instances in your Auto Scaling Group (ASG). While updates to the ASG automatically apply to newly launched instances, an instance refresh is required to apply these changes to instances that are already running. This ensures that all instances in your ASG are consistent with the latest settings.

In general, this feature works for:

* **ASGs with EC2 Instances**: It applies to Auto Scaling Groups that are managing EC2 instances, which can be part of a Kubernetes cluster.
* **ASGs using Launch Templates or Configurations**: The ASG must be configured to use a launch template or configuration to define how new instances should be created.

## Initiating an **Instance Refresh** for an **Auto Scaling Group (ASG)**

1. Select the appropriate Tenant from the **Tenant** list box.
2. For Kubernetes-managed ASGs (Nodes), navigate to **Kubernetes** -> **Nodes**. For Docker Native ASGs (EC2 Instances Running Docker Directly), Navigate to **Cloud Services** -> **Hosts**.
3. Select the **ASG** tab.
4. Select the name of the ASG you want to refresh from the **NAME** column.&#x20;
5. Select the **Launch Template** tab.
6. Click on the **Actions** menu, and select **Start Instance Refresh**. The **Start Instance Refresh** pane displays.

<div align="left"><figure><img src="../../../../../../.gitbook/assets/instance refresh pane.png" alt="" width="344"><figcaption><p>The <strong>Start Instance Refresh</strong> pane</p></figcaption></figure></div>

7. Choose the **Instance Replacement Method**:
   * **Launch before Termination**: New instances are launched before the old ones are terminated, ensuring capacity is maintained throughout the refresh process and minimizing downtime.
   * **Terminate and Launch**: Old instances are terminated first, and new ones are launched afterward. This method may temporarily reduce capacity until the new instances are fully launched and healthy.
   * **Custom Behavior**: Define a custom instance replacement strategy to meet specific timing or instance replacement policies based on your needs.
8. Set the **Min** and **Max Healthy Percentage**:
   * **Min Healthy Percentage**: Specifies the minimum percentage of instances that must remain healthy during the refresh to avoid capacity issues.
   * **Max Healthy Percentage**: Limits the percentage of instances that can be healthy during the refresh to control how many instances are updated at once.
9. Define the **Instance Warmup** time, which is the duration to wait before considering a newly launched instance as healthy. This ensures the instance has time to fully initialize.
10. Optionally, select **Update and Launch Template** to apply any new configurations to the instances being replaced.
    * **Version**: If updating the launch template, choose the desired version of the launch template to apply to the instances being replaced.
11. Click **Start** to initiate the refresh process. The EC2 instances within the ASG will begin updating according to the selected replacement method.&#x20;

{% hint style="info" %}
**Note**: The instance refresh process can take some time to complete depending on the number of instances and the selected update method. Please allow adequate time for the instances to be updated and replaced.
{% endhint %}
