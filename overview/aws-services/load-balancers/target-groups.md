---
description: Create and manage AWS Target Groups to control application traffic routing
---

# Target Groups

Target Groups route traffic from a Load Balancer to specific backend resources, such as EC2 instances, IP addresses, or other Load Balancers (ALBs).  They’re helpful when you need precise control over traffic distribution, health check monitoring, or when consolidating traffic across multiple services behind a shared ALB.&#x20;

## Prerequisites

A Target Group routes traffic to one or more backend resources, which are the actual systems that process incoming requests. Before creating a Target Group, ensure the appropriate backend resource is already created.&#x20;

Supported backend resource types include:

* **EC2 Instances**: Instances managed within DuploCloud.
* **IP Addresses**: Static IPs for known resources, such as external systems.
* **Internal ALBs (Application Load Balancers)**: ALBs created within DuploCloud. These must already exist and be configured appropriately. Supported internal ALBs include:
  * ALBs created under **Networking** → **Load Balancer**.
  * ALBs provisioned through **Kubernetes** → **Ingress Load Balancer**.
  * ALBs created via **Kubernetes** → **Services** or **Docker** → **Services**.

## Step 1. Creating a Target Group

A Target Group defines how traffic is routed to backend resources. This is a required step before connecting a frontend ALB to internal services such as Kubernetes or Docker workloads.

Follow these steps to create a Target Group:

1. From the DuploCloud Portal, navigate to **Cloud Services** → **Networking** → **Load Balancers**.
2. Select the **Target Groups** tab.
3.  Click **Add**. The **Create Target Group** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (313) (1).png" alt="" width="362"><figcaption><p>The <strong>Create Target Group</strong> pane<br></p></figcaption></figure></div>
4. Complete the following fields:

<table data-header-hidden><thead><tr><th width="204.22222900390625"></th><th></th></tr></thead><tbody><tr><td><strong>Target Group Name</strong></td><td>Provide a unique name for the target group.</td></tr><tr><td><strong>Target type</strong></td><td><p>Specify what kind of backend resource will receive traffic:</p><ul><li>Choose <strong>Instance</strong> to route traffic to EC2 instances.</li><li>Choose <strong>IP</strong> to route traffic to a static IP address.</li><li>Choose <strong>ALB</strong> to route traffic to another load balancer, such as one attached to a Kubernetes or Docker service. </li></ul><p><strong>Note:</strong> When using an ALB as a Target Type, the target group's <strong>port and protocol must match</strong> a listener on the selected ALB. For example, if the target group uses port 30080 with TCP, the ALB must have a listener on port 30080 using TCP.</p></td></tr><tr><td><strong>Port</strong></td><td>Specify the port on which backend resources are listening (must be between <strong>1</strong> and <strong>65535</strong>).</td></tr><tr><td><strong>Protocol</strong></td><td><p>Specify how traffic is routed to targets:</p><ul><li>Select <strong>HTTP</strong> or <strong>HTTPS</strong> if your backend supports Layer 7 routing (e.g., web services).</li><li>Select <strong>TCP</strong> for Layer 4 routing (common with internal ALBs or non-HTTP services).</li></ul></td></tr><tr><td><strong>Health Check Path</strong></td><td>Specify the URL path for health checks (e.g., <code>/health</code>).</td></tr><tr><td><strong>Health Check Protocol</strong></td><td>Select the protocol used for health checks (e.g., <strong>HTTPS</strong>, <strong>TCP</strong>, etc.).</td></tr><tr><td><strong>HTTP Success Code</strong></td><td>Enter the HTTP Success Code that indicates a healthy response (e.g., <code>200</code>, <code>200-299</code>).</td></tr></tbody></table>

5. Click **Add** to create the Target Group.

## Step 2. Registering Targets

Register backend resources to your Target Group. Registered targets will receive traffic routed by the Load Balancer. You can register EC2 Instances, IP addresses, or ALB Load Balancers.

1. From the DuploCloud Portal, navigate to **Cloud Services** → **Networking** → **Load Balancers**.
2. Select the **Target Groups** tab.&#x20;
3. Click the menu icon (<img src="../../../.gitbook/assets/menu icon (4).avif" alt="" data-size="line">) in the row of the Target Group.
4.  Select **Register Targets**. The **Register Targets** pane displays. \


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (117).png" alt="" width="344"><figcaption><p>The <strong>Register Targets</strong> pane with an Instance selected</p></figcaption></figure></div>
5. In the **Register Targets** pane, specify the Targets you want to register:
   * **Instance:** Select an EC2 Instance from the **Targets** list box.
   * **IP Address:** Enter the IP Address in the **Add IP address** field.
   * **ALB:** Select an Application Load Balancer (ALB) from the **Targets** list box.
6. Click **Register**. The target(s) are registered to the Target Group.

## Step 3. Creating a Load Balancer

To route traffic to your Target Group, create an Application Load Balancer (ALB) and associate it with the appropriate Target Group.

1. From the DuploCloud Portal, navigate to **Cloud Services** → **Networking** → **Load Balancers**.
2. Select the **Load Balancers** tab.
3. Click **Add**. The **Create a Load Balancer** pane displays.
4. Complete the required fields as shown below:

<table data-header-hidden><thead><tr><th width="174"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Provide a unique name for the Load Balancer. </td></tr><tr><td><strong>Type</strong></td><td>Choose your Load Balancer type (e.g., <strong>Network</strong> or <strong>Application</strong>).</td></tr><tr><td><strong>Visibility</strong></td><td>Select <strong>Public</strong> to make the Load Balancer accessible from the internet, or <strong>Internal</strong> to restrict access to within your private network or VPC.</td></tr></tbody></table>

5. Click **Create** to create the Load Balancer.
6. Once the Load Balancer is created, add a listener:
   * On the **Load Balancers** page, select your newly created Load Balancer, and click on the **Listeners** tab.&#x20;
   * Click **Add**. The **Add Load Balancer Listener** page displays.
   * Complete the fields in the **Add Load Balancer Listener** page as shown below:

<table data-header-hidden><thead><tr><th width="196.22222900390625"></th><th></th></tr></thead><tbody><tr><td><strong>Port</strong></td><td>Provide the Load Balancer Listener Port (e.g., <strong>80</strong> for HTTP or <strong>443</strong> for HTTPS).</td></tr><tr><td><strong>Protocol</strong></td><td>Choose the same protocol used by the Target Group (e.g., <strong>TCP</strong>, <strong>TLS</strong>, or <strong>UDP</strong>) to ensure compatibility.</td></tr><tr><td><strong>Action Type</strong></td><td>Choose <strong>Forward to target groups</strong>.</td></tr><tr><td><strong>Forward Target Group</strong></td><td>Select the Target Group created in step 1.  </td></tr></tbody></table>

7. Click **Save** to create the listener. The Load Balancer will route traffic to the selected Target Group based on the configured listener rules and health checks.

## Managing Target Groups

You can update your Target Group configurations directly from Target Group menu:

1. From the DuploCloud Portal, navigate to **Cloud Services** → **Networking** → **Load Balancers**.
2. Select the **Target Groups** tab.
3. Click the **menu icon** (<img src="../../../.gitbook/assets/image (466).png" alt="" data-size="line">) next to the Target Group you want to edit.
4. Select from the following options:&#x20;

<table data-header-hidden><thead><tr><th width="193.55560302734375"></th><th></th></tr></thead><tbody><tr><td><strong>Console</strong></td><td>Access the Azure Console </td></tr><tr><td><strong>Edit</strong></td><td>Modify the Target Group settings</td></tr><tr><td><strong>Register Targets</strong></td><td>Register target(s) from the Target Group</td></tr><tr><td><strong>Deregister Targets</strong></td><td>Deregister target(s) from the Target Group</td></tr><tr><td><strong>Delete</strong></td><td>Permanently removes the Target Group</td></tr></tbody></table>

6. Click **Update**. The changes are applied.
