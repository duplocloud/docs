---
description: Managing EC2 hosts in DuploCloud AWS
---

# Hosts (VMs)

Once you have the Infrastructure (Networking, Kubernetes cluster, and other common configurations) and an environment (Tenant) set up, the next step is to launch EC2 virtual machines (VMs). You create VMs to be:

* EKS Worker Nodes
* Worker Nodes (Docker Host), if the built-in container orchestration is used.

You also create VMs if Regular nodes are not part of any container orchestration; for example, where a user manually connects and installs apps, as when using Microsoft SQL Server in a VM, Running an IIS application, and such custom use cases.

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
