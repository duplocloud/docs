---
description: Add a Host (VM) in the DuploCloud Portal.
---

# Adding Hosts

In DuploCloud, a Host represents a virtual machine (VM) that runs your workloads in the cloud. DuploCloud supports multiple Host types on AWS, including:

* Individual EC2 instances
* Auto Scaling Groups (ASGs) for scalable clusters
* Bring Your Own Host (BYOH) for integrating existing or non-standard VMs

Use BYOH for any Host that is neither EC2 nor ASG.

## Adding a Host (VM)

### Adding an EC2 Host

1. Select the appropriate Tenant from the **Tenant** list box.
2. Navigate to **Cloud Services** -> **Hosts**.&#x20;
3. Select the **EC2** tab.
4.  Click **Add**. The **Add Host** page displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (782).png" alt=""><figcaption><p><strong>Add Host</strong> page</p></figcaption></figure></div>
5. Complete the required fields:

<table data-header-hidden><thead><tr><th width="232.66668701171875">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Friendly Name</strong></td><td>Enter a descriptive name for the Host.</td></tr><tr><td><strong>Availability Zone</strong></td><td>Select an availability zone or choose <strong>Automatic</strong> to let AWS decide.</td></tr><tr><td><strong>Instance Type</strong></td><td>Select the EC2 instance type (e.g., <strong>2 CPU 2 GB - t3a.small</strong>)<br>Only instance types that do not exceed the quotas defined for this Plan are available. You cannot create EC2 hosts that exceed these quotas. For more information, see <a href="../resource-quotas.md">Resource Quotas</a>.</td></tr></tbody></table>

6. Optionally, select **Advanced Options** and complete the additional configurations:

<table data-header-hidden><thead><tr><th width="228.22222900390625">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Agent Platform</strong></td><td>Select the Agent Platform, such as <strong>EKS Linux</strong> or <strong>Docker Windows</strong>.</td></tr><tr><td><strong>Image ID</strong></td><td>The Image ID is auto-populated based on the Agent Platform; override it if needed.</td></tr><tr><td><strong>Dedicated Host ID</strong></td><td>Specify the Dedicated Host ID, e.g., <code>h-0c6ab6f38bdcb24f6</code>. This ID is used to launch an instance on the Host. </td></tr><tr><td><strong>Allocation Tags</strong></td><td>Add Allocation Tags to manage where workloads are scheduled within the infrastructure.</td></tr><tr><td><strong>Disk Size</strong></td><td>Enter the EBS volume size in GB. If not specified, the volume size will be the same as defined in the AMI.</td></tr><tr><td><strong>Enable Storage Encryption</strong></td><td>Select <strong>Yes</strong> to encrypt the root volume, or <strong>No</strong> to leave it unencrypted.</td></tr><tr><td><strong>Key Pair Type</strong></td><td>Select the Key Pair Type. Supported types are <strong>ED25519</strong> and <strong>RSA</strong>. The default is <strong>ED25519</strong>.</td></tr><tr><td><strong>Enable Block EBS Optimization</strong></td><td>Select <strong>Yes</strong> to enable optimized EBS performance, or <strong>No</strong> to disable it.</td></tr><tr><td><strong>Enable Hibernation</strong></td><td>Select <strong>Yes</strong> to allow EC2 hibernation; select <strong>No</strong> to disable it.</td></tr><tr><td><strong>Metadata service</strong></td><td>Select <strong>V1 and V2 Enabled</strong>, <strong>V2 Only Enabled</strong>, or <strong>Disabled</strong> to manage instance metadata access. Default is <strong>V2 Only Enabled</strong>.</td></tr><tr><td><strong>Prepend Duplo's userdata to my custom userdata</strong></td><td>Select this option to prepend DuploCloud’s bootstrap scripts before your custom user data.</td></tr><tr><td><strong>Base64 Data</strong></td><td><p>Enter Base64-encoded data strings (for example, a startup script). On Linux, encode your script using:</p><p><code>cat &#x3C;filepath> | base64 -w 0</code> .</p></td></tr><tr><td><strong>Volumes</strong></td><td>Specify additional storage volumes (in JSON format) to attach to the Host. </td></tr><tr><td><strong>Tags</strong></td><td>Enter AWS Tags as JSON key-value pairs to apply to the EC2 instance.</td></tr><tr><td><strong>Node Labels</strong></td><td>Optionally, enter Kubernetes Node Labels as key-value pairs to apply to this Host (for EKS Hosts only).</td></tr></tbody></table>

7. Click **Add**. The Host will appear on the **EC2** tab.

To connect to the Host using SSH, [follow this procedure](ssh-ec2-instance.md).

{% hint style="info" %}
The EKS **Image ID** is the image published by AWS specifically for an EKS worker in the version of Kubernetes deployed at Infrastructure creation time.

If no **Image ID** is available with a prefix of **EKS**, copy the **AMI ID** for the desired EKS version by referring to this [AWS documentation](https://docs.aws.amazon.com/eks/latest/userguide/eks-optimized-amis.html). Select **Other** from the **Image ID** list box and paste the copied **AMI ID** in the **Other Image ID** field. Contact the DuploCloud Support team via your Slack channel if you have questions or issues.
{% endhint %}

### Adding an Auto Scaling Group (ASG) Host

An Auto Scaling Group (ASG) Host represents a scalable cluster of EC2 instances managed as a group. DuploCloud integrates with AWS Auto Scaling to automatically adjust capacity based on demand.

1. Select the appropriate Tenant from the **Tenant** list box.
2. Navigate to **Cloud Services** -> **Hosts**.&#x20;
3. Select the **ASG** tab.
4.  Click **Add**. The **Add ASG** page displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (783).png" alt=""><figcaption><p><strong>Add ASG</strong> page</p></figcaption></figure></div>
5. Configure the basic ASG settings:

<table data-header-hidden><thead><tr><th width="211.3333740234375">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Friendly Name</strong></td><td>Enter a name to identify the ASG.</td></tr><tr><td><strong>Availability Zones</strong></td><td>Select an Availability Zone or choose <strong>Automatic</strong> to let AWS decide.</td></tr><tr><td><strong>Instance Type</strong></td><td>Select the Instance Type for the ASG instances (e.g., <strong>2 CPU 2 GB - t3a.small</strong>).</td></tr><tr><td><strong>Instance Count</strong></td><td>Enter the desired instance count for the autoscaling group.</td></tr><tr><td><strong>Minimum Instances</strong></td><td>Enter the minimum number of instances allowed.</td></tr><tr><td><strong>Maximum Instances</strong></td><td>Enter the maximum number of instances allowed.</td></tr><tr><td><strong>Use for Cluster Autoscaling</strong></td><td>Select this option to allow the Kubernetes Cluster Autoscaler to manage scaling for this cluster.</td></tr></tbody></table>

6. Optionally, select **Advanced Options** and complete the additional configurations:

<table data-header-hidden><thead><tr><th width="209.5555419921875">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Agent Platform</strong></td><td>Select the Agent Platform (e.g., <strong>EKS Linux</strong>, or <strong>Docker Windows</strong>).</td></tr><tr><td><strong>Image ID</strong></td><td>The Image ID is auto-populated based on the Agent Platform; override it if needed.</td></tr><tr><td><strong>Allocation Tags</strong></td><td>Add Allocation Tags to manage where workloads are scheduled within the infrastructure.</td></tr><tr><td><strong>Disk Size</strong></td><td>Enter the EBS volume size in GB. If not specified, the volume size will be the same as defined in the AMI.</td></tr><tr><td><strong>Enable Storage Encryption</strong></td><td>Select <strong>Yes</strong> to encrypt the root volume, or <strong>No</strong> to leave it unencrypted.</td></tr><tr><td><strong>Key Pair Type</strong></td><td>Select the key pair type. Supported types are <strong>ED25519</strong> and <strong>RSA</strong>. The default is <strong>ED25519</strong>.</td></tr><tr><td><strong>Enable Block EBS Optimization</strong></td><td>Select <strong>Yes</strong> to enable optimized EBS performance, or <strong>No</strong> to disable it.</td></tr><tr><td><strong>Enable Hibernation</strong></td><td>Select <strong>Yes</strong> to allow EC2 hibernation; select <strong>No</strong> to disable it.</td></tr><tr><td><strong>Metadata service</strong></td><td>Select <strong>V1 and V2 Enabled</strong>, <strong>V2 Only Enabled</strong>, or <strong>Disabled</strong> to manage instance metadata access. Default is <strong>V2 Only Enabled</strong>.</td></tr><tr><td><strong>Use Spot Instances</strong></td><td>Select to launch hosts using Spot Instances.</td></tr><tr><td><strong>Scale from zero (BETA)</strong></td><td>Enable the Scale From Zero (BETA) feature.</td></tr><tr><td><strong>Enabled Metrics</strong></td><td>Select this option to enable Auto Scaling Group metrics collection.</td></tr><tr><td><strong>Prepend Duplo's userdata to my custom userdata</strong></td><td>Select this option to prepend DuploCloud’s bootstrap scripts before your custom user data.</td></tr><tr><td><strong>Base64 Data</strong></td><td><p>Enter Base64-encoded data strings (for example, a startup script). On Linux, encode your script using:</p><p><code>cat &#x3C;filepath> | base64 -w 0</code> .</p></td></tr><tr><td><strong>Volumes</strong></td><td>Specify additional storage volumes (in JSON format) to attach to the Host. </td></tr><tr><td><strong>Tags</strong></td><td>Enter Tags as JSON key-value pairs to apply to the ASG.</td></tr><tr><td><strong>Node Labels</strong></td><td>Optionally, enter Kubernetes node labels as key-value pairs to apply to this Host (for EKS Hosts only).</td></tr></tbody></table>

7. Click **Add**. The Host will appear on the **ASG** tab. For information about more advanced features, such as Launch Templates, see the [Auto Scaling Groups (ASG) documentation](auto-scaling/auto-scaling-groups/).

### Adding a BYOH Host

Bring Your Own Host (BYOH) allows you to register and manage existing servers or virtual machines with DuploCloud without provisioning resources through AWS.

1. Select the appropriate Tenant from the **Tenant** list box.
2. Navigate to **Cloud Services** -> **Hosts**.&#x20;
3. Select the **BYOH** tab.
4.  Click **Add**. The **Add** page displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (785) (1).png" alt=""><figcaption><p><strong>Add</strong> page</p></figcaption></figure></div>
5. Complete the following fields:

<table data-header-hidden><thead><tr><th width="195.33331298828125">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Friendly Name</strong></td><td>Enter a descriptive name for the Host.</td></tr><tr><td><strong>Direct Address</strong></td><td>Enter the IPv4 address that DuploCloud will use to communicate with the agent installed on your Host.</td></tr><tr><td><strong>Fleet Type</strong></td><td>Select the Fleet Type that corresponds to the container orchestrator running on your Host (e.g., <strong>Linux Docker/Native</strong>, <strong>Docker Windows</strong>, or <strong>None</strong>).</td></tr><tr><td><strong>Username</strong></td><td>Optionally, enter the Username for your Host.</td></tr><tr><td><strong>Password</strong></td><td>Optionally, enter the Password for access.</td></tr><tr><td><strong>Private Key</strong></td><td>Optionally, enter the Private Key used to log in to your Host via SSH. You can specify either a Password or a Private Key for authentication.</td></tr></tbody></table>

6. Click **Add**. The Host will appear on the **BYOH** tab.

## Creating Kubernetes StorageClass and PVC constructs in the DuploCloud Portal.

See [Kubernetes StorageClass and PVC](../../../kubernetes-overview/kubernetes-storageclass-and-pvc/).

## Supported Host Actions

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Hosts**.&#x20;
2. Select the **Host** name from the list.
3. From the **Actions** list box, you can select **Connect**, **Host Settings**, or **Host State** to perform the following supported actions:&#x20;

### **Connect:**

<table data-header-hidden><thead><tr><th width="180"></th><th></th></tr></thead><tbody><tr><td><strong>SSH</strong></td><td>Establish an <a href="ssh-ec2-instance.md#connecting-to-an-ec2-linux-instance-using-ssh">SSH connection</a> to work directly in the AWS Console.</td></tr><tr><td><strong>Connection Details</strong></td><td>View connection details (connection type, address, user name, visibility) and <a href="ssh-ec2-instance.md#connect-by-downloading-a-key">download the key</a>.</td></tr><tr><td><strong>Host Details</strong></td><td>View Host details in the <strong>Host Details</strong> JSON screen.</td></tr></tbody></table>

<div align="left"><figure><img src="../../../.gitbook/assets/Shot 1 connection.png" alt=""><figcaption><p>The Host <strong>Actions</strong> menu with <strong>Connect</strong> selected.</p></figcaption></figure></div>

### **Host Settings:**

<table data-header-hidden><thead><tr><th width="208"></th><th></th></tr></thead><tbody><tr><td><strong>Create AMI</strong></td><td>Create an <a href="create-amazon-machine-image-ami.md">AMI</a> from the Host. </td></tr><tr><td><strong>Create Snapshot</strong></td><td>Create a <a href="ec2-snapshots.md">snapshot </a>of the Host at a specific point. </td></tr><tr><td><strong>Update User Data</strong></td><td>Update the Host user data.</td></tr><tr><td><strong>Change Instance Size</strong></td><td>Resize a Host instance to accommodate the workload. </td></tr><tr><td><strong>Update Auto Reboot Status Check</strong></td><td>Enable or disable <a href="configure-auto-reboot.md">Auto Reboot</a>. Set the number of minutes after the AWS Instance Status Check fails before automatically rebooting. Also allows updating the Auto Reboot setting if the instance is disconnected.</td></tr></tbody></table>

<div align="left"><figure><img src="../../../.gitbook/assets/Shot 2 Host Connections.png" alt=""><figcaption><p>The Host <strong>Actions</strong> menu with <strong>Host Settings</strong> selected.</p></figcaption></figure></div>

### **Host State:**

<table data-header-hidden><thead><tr><th width="163"></th><th></th></tr></thead><tbody><tr><td><strong>Start</strong></td><td>Start the Host.</td></tr><tr><td><strong>Reboot</strong></td><td>Reboot the Host.</td></tr><tr><td><strong>Stop</strong> </td><td>Stop the Host. </td></tr><tr><td><strong>Hibernate</strong></td><td>Temporarily freeze (hibernate) the Host.</td></tr><tr><td><strong>Terminate Host</strong></td><td>Terminate the Host. </td></tr></tbody></table>

<div align="left"><figure><img src="../../../.gitbook/assets/Shot 3 Host State.png" alt=""><figcaption><p>The Host <strong>Actions</strong> menu with <strong>Host State</strong> selected.</p></figcaption></figure></div>

## Adding custom code for EC2 or ASG Hosts&#x20;

If you add custom code for EC2 or ASG Hosts using the **Base64 Data** field, your custom code overrides the code needed to start the EC2 or ASG Hosts and the Hosts cannot connect to EKS. Instead, [use this procedure](adding-hosts.md#adding-custom-code-for-ec2-and-asg-hosts-in-eks) to add custom code directly in EKS.&#x20;

```bash
#!/bin/bash
set -o xtrace
/etc/eks/bootstrap.sh duploinfra-MYINFRA --kubelet-extra-args '--node-labels=tenantname=duploservices-MYTENANT'

# Custom user code:
echo "hello world"
```

