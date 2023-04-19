---
description: Upgrade the Elastic Kubernetes Service (EKS) version for AWS
---

# Upgrading the EKS version

AWS frequently updates the version of EKS based on new features that are available in the Kubernetes platform. DuploCloud automates this upgrade in the DuploCloud Portal.

{% hint style="warning" %}
**IMPORTANT: An EKS version upgrade can cause downtime to your application depending on the number of replicas you have configured for your services. Schedule this upgrade outside of your business hours to minimize disruption.**
{% endhint %}

### About the upgrade process

The upgrade process:

* Updates the EKS Control Plane to the latest version
* Relaunches all Hosts to deploy the latest version on all nodes.

After the upgrade process completes successfully, you optionally assign allocation tags to Hosts.

### Starting the upgrade&#x20;

To upgrade the EKS version, in the DuploCloud Portal:&#x20;

1. Click **Administrator** -> **Infrastructure.**
2. Select the Infrastructure that you want to upgrade to the latest EKS version.
3. Select the **EKS** tab. If an Infrastructure upgrade is available, **Upgrade** appears in the **Value** column.
4. Click **Upgrade**.

![EKS tab with Upgrade available](../../../.gitbook/assets/AWS\_EKS\_Tab\_041923.png)

### Monitoring the upgrade&#x20;

Monitor the upgrade by using the **EKS Upgrade Details** screen.

![EKS Upgrade Details screen and the Status list](<../../../.gitbook/assets/Screen Shot 2022-07-16 at 4.58.59 PM.png>)

### Upgrade completion

The **EKS Upgrade Details** screen displays the progress of updates for all versions and Hosts. Green checkmarks indicate successful completion in the **Status** list.

### Assign allocation tags

If any of your Hosts use allocation tags, you must assign allocation tags to the Hosts:

1. After your Hosts are online and available, navigate to **DevOps** -> **Hosts**.
2. Select the host group tab (**EC2**, **ASG**, etc.) on the **Hosts** screen.&#x20;
3. Click the **Add** button.
4. Name the Host and provide other configuration details on the **Add Host** form.
5. Select **Advanced Options**.
6. Edit the **Allocation Tag** field.&#x20;
7. Click **Create** and define your allocation tags.
8. Click **Add** to assign the allocation tags to the Host.

<figure><img src="../../../.gitbook/assets/Hosts_Tags_AWS.png" alt=""><figcaption><p>Allocation tags in the <strong>Add Host</strong> screen</p></figcaption></figure>

&#x20;                                    &#x20;
