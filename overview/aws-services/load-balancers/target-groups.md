---
description: Create and manage AWS Target Groups to control application traffic routing
---

# Target Groups

Target Groups route traffic from a Load Balancer to specific backend resources, such as EC2 instances, IP addresses, or other Load Balancers (ALBs). They allow fine-grained control over request routing and health checks.

## Prerequisites

Before creating a Target Group, ensure the necessary resources are created and available. The types of targets you can register include **EC2 Instances**, **ALBs (Application Load Balancers)**, and **IP addresses**.&#x20;

You can find detailed instructions for creating these resources in the DuploCloud documentation:

* [**EC2 Instances**](../../use-cases/hosts-vms/adding-hosts.md)
* [**ALBs (Application Load Balancers)**](./#creating-a-shared-load-balancer-for-the-target-group)
* **IP Addresses**: DuploCloud allows the use of IP addresses assigned to EC2 instances or other resources. Ensure the required IP addresses are available.

## Creating Target Groups

To create a Target Group, complete the following steps:

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Networking** -> **Load Balancers**.
2. Select the **Target Groups** tab.
3.  Click **Add**. The **Create Target Group** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (313) (1).png" alt="" width="362"><figcaption><p>The <strong>Create Target Group</strong> pane<br></p></figcaption></figure></div>
4. Complete the fields:

<table data-header-hidden><thead><tr><th width="218.4444580078125"></th><th></th></tr></thead><tbody><tr><td><strong>Target Group Name</strong></td><td>A unique name to identify the target group.</td></tr><tr><td><strong>Port</strong></td><td>Port number to route traffic to (must be between <code>1</code> and <code>65535</code>).</td></tr><tr><td><strong>Protocol</strong></td><td>Protocol used for routing traffic (e.g., <code>HTTP</code>, <code>HTTPS</code>, <code>TCP</code>).</td></tr><tr><td><strong>Health Check Path</strong></td><td>The URL path for health checks (e.g., <code>/health</code>).</td></tr><tr><td><strong>Health Check Protocol</strong></td><td>Protocol used for health checks (e.g., <code>HTTPS</code>, <code>TCP</code>, etc.).</td></tr><tr><td><strong>HTTP Success Code</strong></td><td>The HTTP Success Code that indicates a healthy response (e.g., <code>200</code>, <code>200-299</code>).</td></tr></tbody></table>

5. Click **Add** to create the Target Group.

## Registering Targets

Register backend resources to your Target Group. Registered targets will receive traffic routed by the Load Balancer. You can register EC2 Instances, IP addresses, or ALB Load Balancers.

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Networking** -> **Load Balancers**.
2. Select the **Target Groups** tab.&#x20;
3. Click the menu icon (<img src="../../../.gitbook/assets/menu icon (4).avif" alt="" data-size="line">) in the row of the the Target Group.
4.  Select **Register Targets**. The **Register Targets** pane displays. \


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (117).png" alt="" width="344"><figcaption><p>The <strong>Register Targets</strong> pane with an Instance selected</p></figcaption></figure></div>
5. Specify the **Targets** you want to register.
6. Click **Register**. The target(s) are registered to the Target Group.

## Managing Target Groups

Manage Target Groups directly from the menu options in the Target Groups tab:

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Networking** -> **Load Balancers**.
2. Select the **Target Groups** tab.
3. Click the **menu icon** (<img src="../../../.gitbook/assets/image (466).png" alt="" data-size="line">) next to the Target Group you want to edit.
4. Select from the following options:&#x20;

<table data-header-hidden><thead><tr><th width="193.55560302734375"></th><th></th></tr></thead><tbody><tr><td><strong>Console</strong></td><td>Access the Azure Console </td></tr><tr><td><strong>Edit</strong></td><td>Modify the Target Group settings</td></tr><tr><td><strong>Register Targets</strong></td><td>Register target(s) from the Target Group</td></tr><tr><td><strong>Deregister Targets</strong></td><td>Deregister target(s) from the Target Group</td></tr><tr><td><strong>Delete</strong></td><td>Permanently removes the Target Group</td></tr></tbody></table>

6. Click **Update**. The changes are applied.
