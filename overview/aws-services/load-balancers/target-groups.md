---
description: Create and manage AWS Target Groups to control application traffic routing
---

# Target Groups

Target Groups route traffic from a Load Balancer to specific backend resources, such as EC2 instances, IP addresses, or other Load Balancers (ALBs). They allow fine-grained control over request routing and health checks.

## Creating Target Groups

Create a Target Group, where you can define the resources, protocols, and health check settings for efficient traffic routing.

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Networking** -> **Load Balancers**.
2. Select the **Target Groups** tab.
3.  Click **Add**. The **Create Target Group** pane displays.\
    \


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (118).png" alt="" width="336"><figcaption><p>The <strong>Create Target Group</strong> pane<br></p></figcaption></figure></div>
4. Complete the following fields:
   * **Name:** Give the Target Group a unique name
   * **Target type**: Select the target type for your needs:
     * **Instance:** For EC2 instances.
     * **IP:** For specific IP addresses.
     * **ALB:** For registering another Load Balancer.
   * **Port number** and **Protocol**: Choose the port and protocol for communication.
   * **Health Checks**: Set up health check criteria to monitor target health.
5. Click **Add** to create the Target Group.

## Registering Targets

Register backend resources to your Target Group. Registered targets will receive traffic routed by the Load Balancer. You can register the following types of targets:

* **EC2 Instances**
* **IP addresses**
* **ALB Load Balancers\***

{% hint style="warning" %}
\*Before registering an ALB as a target, you must first [create a Load Balancer](./#adding-a-shared-load-balancer) (from the Networking tab) and [add a listener](./#creating-a-shared-load-balancer-for-the-target-group). Only then can you register the ALB to your Target Group.
{% endhint %}

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Networking** -> **Load Balancers**.
2. Select the **Target Groups** tab.&#x20;
3. Click the menu icon (<img src="../../../.gitbook/assets/menu icon (4).avif" alt="" data-size="line">) next to the Target Group where you want to register targets.
4.  Select **Register Targets**. The **Register Targets** pane displays. \


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (117).png" alt="" width="344"><figcaption><p>The <strong>Register Targets</strong> pane with an Instance selected</p></figcaption></figure></div>
5. In the **Target** field, specify the target:
   * **For EC2 Instance Type**: Select the Instance from the **Target** list box.&#x20;
   * **For IP Type**: Enter the IP address of the resource in the **Add IP Address** field.
   * **For ALB Type**: Select the ALB from the **Target** list box.&#x20;
6. Click **Register**. The target is registered to the Target Group.

## Managing Target Groups

You can manage your Target Groups by editing, deregistering targets, or deleting them directly from the menu options in the Target Groups tab.

### **Editing a Target Group**

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Networking** -> **Load Balancers**.
2. Select the **Target Groups** tab.
3. Click the menu icon (<img src="../../../.gitbook/assets/image (466).png" alt="" data-size="line">) next to the Target Group you want to edit.
4. Select **Edit**.
5. Make the necessary changes to the Target Group settings (e.g., health check path).
6. Click **Update**. The changes are applied.

### **Deregistering Targets**

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Networking** -> **Load Balancers**.
2. Select the **Target Groups** tab.
3. Click the menu icon (<img src="../../../.gitbook/assets/image (466).png" alt="" data-size="line">) next to the Target Group where you want to deregister targets.
4. Select **Deregister Targets**. The **Deregister Targets** pane displays.
5. In the **Targets** list box, select the target you wish to remove.
6. Click **Deregister**. The selected target is deregistered from the Target Group.

### **Deleting a Target Group**

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Networking** -> **Load Balancers**.
2. Select the **Target Groups** tab.
3. Click the menu icon (<img src="../../../.gitbook/assets/image (466).png" alt="" data-size="line">) next to the Target Group you want to delete.
4. Select **Delete**.
5. Click **Confirm** to confirm the deletion. The Target Group is permanently removed.
