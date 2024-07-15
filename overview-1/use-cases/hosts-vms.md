---
description: Using Hosts in DuploCloud
---

# Hosts (VMs)

Once we have the Infrastructure (Networking, Kubernetes cluster, and other common configurations) and an environment (Tenant) set up, the next step is to create VMs. These could be meant for:

* Compute Engine virtual machines in GCP
* Worker Nodes (Docker Hosts) if built-in container orchestration is used.
* Regular nodes that are not part of any container orchestration, where a user manually connects and installs applications.&#x20;

## Adding a GCP Host <a href="#id-3-toc-title" id="id-3-toc-title"></a>

In GCP, you can use GCE VMs or BYOH (bring your own hosts) to get a Virtual Machine setup. Both of these are available through the **Cloud Services -> Hosts** menu

See the Services documentation for steps to [create Hosts and configure Kubernetes storage options](../gcp-services/containers/).&#x20;

<div align="left">

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-12 at 5.21.26 PM.png" alt=""><figcaption><p>Hosts in GCP</p></figcaption></figure>

</div>

### GCE VM

You can create a GCE VM by going to **Cloud Services** -> **Hosts** ->  **GCE VM**.

<div align="left">

<figure><img src="../../.gitbook/assets/virtual machine add.png" alt=""><figcaption><p><strong>Add GCE Virtual Machine</strong> page</p></figcaption></figure>

</div>

### BYOH Host

While lower-level details such as IAM roles and security groups are abstracted, deriving instead from the Tenant, only the most application-centric inputs are required to set up Hosts.&#x20;

<div align="left">

<figure><img src="../../.gitbook/assets/GCP_HOSTS_Add_BYOH (1).png" alt=""><figcaption><p><strong>Add BYOH Hosts</strong> page </p></figcaption></figure>

</div>

Most of these inputs are optional and some are available as list box selections, set by the administrator in the Plan (for example, **Image ID**, in Host **Advanced Options**).&#x20;

There is an additional parameter labeled **Fleet Type**. This is applicable if the VM is to be used as a host for [container orchestration](../container-deployments/container-orchestrators.md) by the platform. The choices are:

* **Linux Docker/Native**: To be used for hosting Linux containers using the Built-in Container orchestration.      &#x20;
* **None**: To be used for non-Container Orchestration purposes and contents inside the VM are self-managed by the user.

{% hint style="info" %}
If a VM is used for container orchestration, ensure that the **Image ID** corresponds to the Image in the container. Any name that begins with **Duplo** is an image that DuploCloud generates for Built-in container orchestration &#x20;
{% endhint %}

## Increasing minimum ports per VM instance (GKE Standard)

You can increase the number of available ephemeral ports per GKE Standard VM instance in the DuploCloud Portal using Infrastructure systems settings. More ports help handle high volumes of network traffic, especially for applications that require many simultaneous connections.

To increase the minimum ports per VM for your Infrastructure:&#x20;

* Navigate to **Administrator** -> **Infrastructure**.
* In the **NAME** column, select your Infrastructure name.&#x20;
* Select the **Settings** tab, and click **Add**. The **Infra - Set Custom Data** pane displays.
* From the **Setting Name** list box, select **GKE Minimum Ports Per VM**.&#x20;
* In the **Setting Value** field, enter the minimum number of ports you want or each VM.&#x20;
*   Click **Set**. VMs in this Infrastructure will have at least the minimum number of ports configured. \


    <figure><img src="../../.gitbook/assets/minimum ports per VM.png" alt=""><figcaption></figcaption></figure>
