---
description: Adding EC2 hosts in DuploCloud AWS
---

# Hosts (VMs)

Once we have the Infrastructure (Networking, Kubernetes cluster, and other common configurations) and an environment (Tenant) setup, the next step is typically to launch EC2 virtual machines (VMs). You create VMs to be:

* EKS Worker Nodes
* Worker Nodes (Docker Host), if the built-in container orchestration is used.

You also create VMs if Regular nodes are not part of any container orchestration; for example, where a user manually connects and installs apps, as when using Microsoft SQL Server in a VM, Running an IIS application, and such custom use cases.

## Adding a Host (VM)

Add a Virtual Machine Host. DuploCloud AWS supports **EC2**, **ASG**, and **BYOH** (Bring Your Own Host) types. Use **BYOH** for any VMs that are not **EC2** or **ASG**.&#x20;

1. Ensure you have selected the appropriate Tenant from the **Tenant** list box at the top of the DuploCloud Portal.
2. In the DuploCloud Portal, navigate to **DevOps -> Hosts**.&#x20;
3. Click the tab that corresponds to the type of Host you want to create (**EC2**, **ASG**, or **BYOH**).
4. Click **Add**.

{% hint style="info" %}
The EKS **Image ID** is the image published by AWS specifically for an EKS worker in the version of Kubernetes deployed at Infrastructure creation time. For this tutorial, the region is **us-west-2**, where the **NONPROD** Infrastructure was created.&#x20;

If no **Image ID** is available with a prefix of **EKS**, copy the **AMI ID** for the desired EKS version by referring to this [AWS documentation](https://docs.aws.amazon.com/eks/latest/userguide/eks-optimized-amis.html). Select **Other** from the **Image ID** list box and paste the copied **AMI ID** in the **Other Image ID** field. Contact the DuploCloud Support team via your Slack channel if you have questions or issues.
{% endhint %}

{% hint style="danger" %}
If you add custom code for EC2 or ASG hosts using the **Base64 Data** field, your custom code overrides the code needed to start the EC2 or ASG hosts and the hosts cannot connect to EKS. Instead, [use this procedure](hosts-vms.md#adding-custom-code-for-ec2-and-asg-hosts-in-eks) to add custom code directly in EKS.&#x20;
{% endhint %}

![Add Host page for EC2](<../../.gitbook/assets/image (17) (1) (1).png>)

While all the lower-level details like IAM roles, Security groups, and others are abstracted away from the user (as they are derived from the Tenant), standard application-centric inputs are required to be provided. This includes a Name, Instance size, Availability Zone choice, Disk size, Image ID, etc. Most of these are optional, some are published as a list of user-friendly choices by the admin in the plan (Image or AMI ID is one such example). Other than these AWS centric parameter there is two DuploCloud platform-specific value to be provided:

**Agent Platform**: This is applicable if the VM is going to be used as a host for [container orchestration](https://docs.duplocloud.com/docs/aws/container-deployments/container-orchestrators) by the platform. The choices are:

* EKS Linux: If this is to be added to the EKS cluster i.e. EKS is the chosen approach for container orchestration
* Linux Docker: If this is to be used for hosting Linux containers using the [Builtin Container orchestration](../container-deployments/)      &#x20;
* Docker Windows: If this is to be used for hosting Windows containers using the [Builtin Container orchestration](../container-deployments/)
* None: If the VM is going to be used for non-Container Orchestration purposes and contents inside the VM will be self-managed by the user

**Allocation Tags (Optional)**: If the VM is being used for containers, then you have the option to set a label on the VM. This label can be then specified during docker app deployment to ensure that the application containers are pinned to a specific set of nodes. Thus you get the ability to split a tenant further into separate pools of servers and deploy applications on them.&#x20;

{% hint style="info" %}
If a VM is being used for container orchestration make sure that the Image ID  corresponds to an Image for that container orchestration. This should be already set up for you and the list box will have self-descriptive Image IDs for example "EKS Worker", "Duplo-Docker", "Windows Docker" etc. Anything that starts with Duplo would be an image for the Built-in container orchestration &#x20;
{% endhint %}

### Connect your EC2 Instance

If you want to connect your EC2 instance remotely using SSH, [follow these steps](../aws-services/virtual-machines/ssh-ec2-instance.md).

## Adding dedicated hosts to launch EC2 instances

Use dedicated hosts to launch Amazon EC2 instances and provide additional visibility and control over how instances are placed on a physical server; enabling you to use the same physical server, if needed

### Prerequisites

Configure the DuploCloud Portal to allow for the creation of dedicated hosts.

1. In the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Click the **System Config** tab.
3.  Click **Add**. The **Add Config** pane displays.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/DH1.png" alt=""><figcaption><p><strong>Add Config</strong> pane with <strong>Key</strong> for <strong>Allow Dedicated Host Sharing</strong> </p></figcaption></figure>

    </div>


4. In the **Config Type** field, select **Flags**.
5. In the **Key** field, select **Allow Dedicated Host Sharing**.
6. In the **Value** field, select **true**.
7. Click **Submit**. The configuration is displayed in the **System Config** tab.

### Creating dedicated hosts to launch EC2 instances

1. In the DuploCloud Portal, navigate to **DevOps** -> **Hosts**.
2. In the EC2 tab, click **Add**. The **Add Host** page displays.
3. After completing the required fields to configure your Host, select **Advanced Options**. The advanced options display.
4.  In the **Dedicated Host ID** field, enter the ID of the dedicated host. The ID is used to launch a specific instance on a dedicated host. See the screenshot below for an example.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/DH2.png" alt=""><figcaption><p><strong>EC2</strong> page with <strong>Advanced Options</strong> displayed including <strong>Dedciated Host ID</strong></p></figcaption></figure>

    </div>


5. Click **Add**. The dedicated host is displayed in the **EC2** tab.

### Viewing dedicated hosts to launch EC2 instances

After you create dedicated hosts, view them by doing the following:

1. In the DuploCloud Portal, navigate to **DevOps** -> **Hosts**.
2.  In the **EC2** tab, select the **Host** from the Name column. The **Dedicated Host ID** card on the Host page displays the ID of the dedicated host.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/DH3.png" alt=""><figcaption><p><strong>Dedicated Host ID</strong> card on the Host page displaying ID of dedicated host</p></figcaption></figure>

    </div>

## Adding custom code for EC2 and ASG hosts in EKS

If you add custom code for EC2 or ASG hosts using the **Base64 Data** field, your custom code overrides the code needed to start the EC2 or ASG hosts and the hosts cannot connect to EKS.&#x20;

To avoid this issue, add the following `bash` command in your EKS instance to include your custom code, replacing:

* MYINFRA with the name of the DuploCloud Infrastructure, and
* MYTENANT with the name of the DuploCloud Tenant

```bash
#!/bin/bash
set -o xtrace
/etc/eks/bootstrap.sh duploinfra-MYINFRA --kubelet-extra-args '--node-labels=tenantname=duploservices-MYTENANT'

# Custom user code:
echo "hello world"
```
