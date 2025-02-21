---
description: Managing Launch Template Versions for Autoscaling Groups (ASG) in DuploCloud
---

# Launch Templates

Launch templates define the configuration for instances in an Auto Scaling Group (ASG). They specify key settings such as the instance type, AMI, and other parameters that determine how new instances are launched. DuploCloud allows you to create multiple launch template versions, each with its own unique settings (e.g., instance type, AMI, etc.). You can easily switch between versions as your requirements evolve. One version can be set as the default, and updates to the launch template can be applied to both new and existing instances by using the[ Instance Refresh feature](instance-refresh-for-asg.md).

This feature is applicable to both Kubernetes Node ASGs and Docker Native ASGs.&#x20;

## Editing launch templates

1. Select the appropriate Tenant from the **Tenant** list box.&#x20;
2. For Kubernetes-managed ASGs (Nodes), navigate to **Kubernetes** -> **Nodes**. For Docker Native ASGs (EC2 Instances Running Docker Directly), Navigate to **Cloud Services** -> **Hosts**.
3. Select the **ASG** tab.&#x20;
4. In the **NAME** column, click on the ASG you wish to edit launch templates for.
5. Select the **Launch Templates** tab.&#x20;
6. In the row of the version you wish to update, click the menu icon (<img src="../../../../../.gitbook/assets/image (459).png" alt="" data-size="line">), and select **Edit (Create a new version)**. The **Edit Launch Template** **(Create a new version)** pane displays.

<div align="left"><figure><img src="../../../../../.gitbook/assets/Screenshot (35).png" alt="" width="398"><figcaption><p>The <strong>Edit Launch Template</strong> <strong>(Create a new version)</strong> pane</p></figcaption></figure></div>

6. Configure the following launch template settings:
   * **Template Version Description**: Provide a description for the new version.
   * **Instance Type**: Select the type of EC2 instance to use for this version (e.g., `t3.medium`, `m5.large`, etc.).
   * **Image ID**: Specify the Amazon Machine Image (AMI) ID for the instances in this version. This defines the base image for launching new instances.
   * **Set as Default**: Optionally, set the newly created version as the **default** launch template for the ASG. The default version automatically applies to all newly launched instances in the ASG.
7. Click **Submit**. The updated launch template version is created.

<div align="left"><figure><img src="../../../../../.gitbook/assets/updated version success.png" alt=""><figcaption></figcaption></figure></div>

## **Changing the default launch template version**

In DuploCloud, you can manage multiple versions of a launch template for your Auto Scaling Group (ASG). You may want to change the default version to ensure that new instances are launched with the desired configuration.

To change the default launch template version:

1. Select the Tenant from the **Tenant** list box.
2. For Kubernetes-managed ASGs (Nodes), navigate to **Kubernetes** -> **Nodes**. For Docker Native ASGs (EC2 Instances Running Docker Directly), Navigate to **Cloud Services** -> **Hosts**.
3. Select the **ASG** tab and click the name of the appropriate ASG.
4. Click on the **Launch Templates** tab.
5. Click the menu icon (<img src="../../../../../.gitbook/assets/image (2) (5).png" alt="" data-size="line">) on the version you want to set as the default.
6. Select **Set as Default**.

The selected version will now be the default for any **new** instances launched in the ASG. Existing instances will remain unchanged. To update existing instances, use the[ Instance Refresh](instance-refresh-for-asg.md) feature.&#x20;
