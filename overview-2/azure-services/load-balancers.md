---
description: Add and configure Load Balancers with DuploCloud Azure
---

# Load Balancers

Load Balancers are essential when running a service. They expose the containers and images in which your application resides. When your containers are run inside a private network, you need a load balancer to listen on the correct ports to access the application. DuploCloud integrates seamlessly with Azure Load Balancers to expose Kubernetes services or Docker containers.

{% hint style="info" %}
DuploCloud allows no more than one (1) Load Balancer per DuploCloud Service.
{% endhint %}

## **Prerequisites**

Before adding a Load Balancer, you need to create the necessary services:

* **For Kubernetes**: See the DuploCloud documentation for [creating an AKS Service](containers-and-services/aks-containers-and-services/#creating-a-duplocloud-aks-service).&#x20;
* **For Docker**: Ensure Docker containers are set up and accessible within your infrastructure. For detailed instructions, see the [DuploCloud documentation](docker-web-application.md#id-2-toc-title).&#x20;

To create a **Shared Application Gateway** Load Balancer, refer to the [Shared Application Gateway](../../kubernetes-overview/ingress-loadbalancer/aks-ingress/) documentation

## Adding a Load Balancer

1. In the DuploCloud Portal, navigate to:
   * **Kubernetes** → **Services** for Kubernetes deployments, or
   * **Docker** → **Services** for Docker deployments.
2. On the **Services** page, select the Service name in the **Name** column.
3. Click the **Load Balancers** tab.
4.  Click **Configure Load Balancer**. The **Add Load Balancer Listener** pane appears.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (334).png" alt="" width="305"><figcaption><p>The <strong>Add Load Balancer Listener</strong> pane</p></figcaption></figure></div>
5. Fill out the required fields based on your configuration needs.
6. Click **Add** to create the Load Balancer.

## Configuring a Load Balancer using rules

Rules define specific configurations for different types of Load Balancers.

For an example of how to configure Load Balancers using rules, see the [Ingress](../../kubernetes-overview/ingress-loadbalancer/aks-ingress/) use case.

## Restricting Open Access to Public Load Balancers

Restrict open access to your public Load Balancers by enforcing controlled access policies.

1. From the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Select the **System Config** tab and click **Add**. The **Add Config** pane displays.

<div align="left"><figure><img src="../../.gitbook/assets/LB flag.png" alt="" width="364"><figcaption><p>The <strong>Add Config</strong> pane in the DuploCloud Portal</p></figcaption></figure></div>

3. From the **Config Type** list box, select **Flags**.
4. From the **Key** list box, select **Deny Open Access To Public LB**.&#x20;
5. In the **Value** list box, select **True**.&#x20;
6. Click **Submit**. Open access to public Load Balancers is restricted.&#x20;
