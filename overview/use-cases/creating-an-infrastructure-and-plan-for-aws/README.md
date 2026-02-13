---
description: Use the DuploCloud Portal to create an AWS Infrastructure and associated Plan
---

# Creating an Infrastructure and Plan for AWS

## Creating an Infrastructure

1.  Click **Add**. The **Add Infrastructure** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (644).png" alt=""><figcaption><p><strong>Add Infrastructure</strong> pane</p></figcaption></figure></div>


2.  Define the Infrastructure by completing the fields:

    <table data-header-hidden><thead><tr><th width="161.55560302734375"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for the infrastructure to identify it within the DuploCloud Portal.</td></tr><tr><td><strong>Cloud</strong></td><td>This is automatically set to AWS and cannot be changed.</td></tr><tr><td><strong>VPC CIDR</strong></td><td>Enter the CIDR block for the new VPC (e.g., <code>10.10.0.0/16</code>). Make sure it doesn’t overlap with existing networks.</td></tr><tr><td><strong>Region</strong></td><td>Select the AWS region where you want to deploy your infrastructure (e.g., <code>us-east-1</code>).</td></tr><tr><td><strong>Availability Zones</strong></td><td>Choose how many AWS availability zones to use. Select more zones for higher availability.</td></tr><tr><td><strong>Subnet CIDR Bits</strong></td><td>Enter the number of CIDR bits to define the size of each subnet (e.g., <code>22</code>). Lower values create larger subnets.</td></tr><tr><td><strong>Enable EKS</strong></td><td>Select this option if you want to deploy a Kubernetes (EKS) cluster in the infrastructure. Once selected, you will be prompted to provide additional EKS settings, such as <strong>Cluster Mode</strong> (<strong>Auto</strong> or <strong>Standard)</strong>, <strong>EKS Version</strong>, <strong>EKS Endpoint Visibility</strong>, <strong>Cluster IP CIDR</strong>, and <strong>EKS logging</strong>. For more information about cluster mode options, see <a href="../../../automation-platform/overview/use-cases/eks-auto-mode.md">EKS Auto Mode</a>. </td></tr><tr><td><strong>Enable ECS Cluster</strong></td><td>Select this option if you want to deploy an ECS cluster for running containerized workloads. Once selected, you can optionally select <strong>Enable Container Insights</strong> for ECS monitoring.</td></tr><tr><td><strong>Advanced Options</strong></td><td>Optionally, expand this section to configure additional network settings. You can enter custom values for <strong>Private Subnet CIDR</strong> and <strong>Public Subnet CIDR</strong> using semicolon-separated CIDR blocks (e.g., <code>10.10.0.0/22;10.10.4.0/22</code>).</td></tr></tbody></table>

    4. Click **Create**. The Infrastructure is created and listed on the **Infrastructure** page. DuploCloud automatically creates a [Plan ](../../../automation-platform/application-focused-interface-duplocloud-architecture/plan.md)(with the same Infrastructure name) with the Infrastructure configuration.&#x20;

<figure><img src="../../../.gitbook/assets/AWS_Infra_new_enable_switches (1).png" alt=""><figcaption><p>AWS <strong>Add Infrastructure</strong> page with highlighted <strong>Enable EKS</strong> and <strong>Enable ECS Cluster</strong> options</p></figcaption></figure>

{% hint style="warning" %}
Cloud providers limit the number of Infrastructures that can run in each region. Refer to your cloud provider for further guidelines on how many Infrastructures you can create.
{% endhint %}

## Viewing Infrastructure settings&#x20;

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**. The **Infrastructure** page displays.&#x20;
2. From the **Name** column, select the Infrastructure containing settings that you want to view.&#x20;
3. Click the **Settings** tab. The Infrastructure settings display.

<figure><img src="../../../.gitbook/assets/eksv (2).png" alt=""><figcaption><p><strong>Settings</strong> tab on the <strong>Infrastructure</strong> page</p></figcaption></figure>

{% hint style="info" %}
Up to one instance (0 or 1) of an EKS or ECS is supported for each DuploCloud Infrastructure.
{% endhint %}

## Configuring EKS features (optional)

You can customize your EKS configuration:

* [Add VPC endpoints](../../../automation-platform/overview/use-cases/creating-an-infrastructure-and-plan-for-aws/add-vpc-endpoints.md).
* Enable EKS endpoints, logs, Cluster Autoscaler, and more. For information about configuration options, see these [EKS Setup](kubernetes-cluster/) topics.&#x20;

## Configuring ECS features (optional)

You can customize your ECS configuration. See the [ECS Setup](../../../automation-platform/overview/use-cases/creating-an-infrastructure-and-plan-for-aws/ecs-setup/) topic for information about configuration options.
