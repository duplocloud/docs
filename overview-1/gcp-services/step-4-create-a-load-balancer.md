---
description: Creating a Load balancer using GCP in DuploCloud
---

# Load Balancers

All containers are running inside a private network and cannot be accessed from an external network. To make them accessible from the an external network, create a Load Balancer.

## Creating a GKE Ingress

If you need to create an Ingress Load Balancer, refer to the [GKE Ingress](../../kubernetes-overview/ingress-loadbalancer/gke-ingress.md) page in the DuploCloud Kubernetes User Guide.&#x20;

## Adding a Load Balancer Listener

{% hint style="info" %}
For an end-to-end example of deploying an application using a GCP Service, see the [GCP Quick start](../quick-start/).
{% endhint %}

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Services**.
2. On the **Services** page, select the Service name in the **Name** column.
3. Click the **Load Balancers** tab.
4. If no Load Balancers exist, click the **Configure Load Balancer** link. If other Load Balancers exist, click **Add** in the **LB listeners** card. The **Add Load Balancer Listener** pane displays.
5. From the **Select Type** list box, select a Load Balancer Listener type based on your Load Balancer.
6. Complete other fields as required and click **Add** to add the Load Balancer Listener.

{% hint style="info" %}
DuploCloud allows no more than one (0 or 1) Load Balancer per DuploCloud Service.
{% endhint %}

<div align="left">

<figure><img src="../../.gitbook/assets/image (12) (5).png" alt=""><figcaption><p>The <strong>Add Load Balancer</strong> pane.</p></figcaption></figure>

</div>
