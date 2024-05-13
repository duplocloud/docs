---
description: Add and configure Load Balancers with DuploCloud Azure
---

# Load Balancers

Load Balancers are essential when running a service. They expose the containers and images in which your application resides. When your containers are run inside a private network, you need a load balancer to listen on the correct ports to access the application.

## Creating an AKS Ingress

If you need to create an Ingress Load Balancer, refer to the[ AKS Ingress](../../kubernetes-overview/ingress-loadbalancer/aks-ingress.md) page in the DuploCloud Kubernetes User Guide.&#x20;

{% hint style="info" %}
DuploCloud allows no more than one (0 or 1) Load Balancer per DuploCloud Service.
{% endhint %}

## Add a Load Balancer Listener&#x20;

Add a load balancer listener that uses the Kubernetes NodePort (K8S NodePort).

Several Load Balancers are available for Azure. See the [Azure Documentation](https://learn.microsoft.com/en-us/azure/load-balancer/skus) for a comparison of each option.

* **Application LB** (Standard load balancer)
* **Shared App Gateway**
* **Classic** (Basic load balancer)
* **Health Check** - Selecting this load balancer allows the **Application LB** (Standard load balancer) to use Kubernetes Health Check to determine whether your service is running properly.

### Before you begin

You must create [Services ](containers-and-services/#adding-a-duplocloud-service)before adding load balancers and listeners. In this example, we name these services **s1-alb** and **s4-nlb**, respectively.&#x20;

<figure><img src="../../.gitbook/assets/AKS_Ingress.png" alt=""><figcaption><p><strong>Services</strong> running ALB and NLB</p></figcaption></figure>

### Adding a Load Balancer Listener

1. In the DuploCloud Portal, navigate **Kubernetes** -> **Services**.
2. On the **Services** page, select the Service name in the **Name** column.
3.  Click the **Load Balancers** tab.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/AKS_Load_Bal.png" alt=""><figcaption><p><strong>Load Balancer</strong> tab on the <strong>AKS Service</strong>s page</p></figcaption></figure>

    </div>
4. Click **Configure Load Balancer**. The **Add Load Balancer Listener** pane appears.
5. Select a type (such as **K8S Node Port)** in the **Select Type** field.&#x20;
6. Add the Kubernetes Health Check URL for this container in the **Health Check** field.&#x20;
7. Complete the other fields in the **Add Load Balancer Listener** and click **Add**.

## Configuring a Load Balancer using rules

Rules specify specific configurations for various types of Load Balancers.

See the [Ingress ](../../kubernetes-overview/ingress-loadbalancer/aks-ingress.md)use case for an example of how to configure Load Balancers using rules.&#x20;
