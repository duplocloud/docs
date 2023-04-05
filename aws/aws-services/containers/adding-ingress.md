---
description: Set up Kubernetes Ingress and Load Balancer with K8s NodePort
---

# Adding Ingress and Load Balancers

## Enable AWS Application Load Balancer&#x20;

Your administrator needs to enable the AWS Application Load Balancer controller for your infrastructure before you can use Ingress.

1. In the DuploCloud Portal, navigate to **Administrator** > **Infrastructure** > _Infrastructure\_name_ > **Settings**.
2. In the **Enable ALB Ingress Controller** field, select **True**.

## Create Tenants, Hosts, and Services with EKS

See the [Containers ](./)topic for steps on how to create [Tenants](../../../getting-started/application-focussed-interface/tenant.md), Hosts, and [Services](../../../getting-started/application-focussed-interface/app-service-and-cloud-service.md).

Once your service is deployed, you are ready to add and configure Kubernetes Ingress.

In this example, three Nginx services run with different paths.

![The Services page](<../../../.gitbook/assets/image (16).png>)

## Add Kubernetes Ingress

Once Services are deployed, add Ingress:

1. Select **DevOpos** -> **Containers -> EKS/Native** from the navigation pane.
2. Click the **K8S Ingress** tab.&#x20;
3. Click **Add**. The **Add Kubernetes Ingress** page displays.

<figure><img src="../../../.gitbook/assets/AWS_Ingress (2).png" alt=""><figcaption><p><strong>Add Kubernetes Ingress</strong> page</p></figcaption></figure>

## Add rules to Kubernetes Ingress

1. In the **Add Kubernetes Ingress** page, configure Ingress by clicking **Add Rule**. The **Add Ingress Rule pane** displays.&#x20;
2. Complete the other fields on the page and click **Add Rule**. Add additional rules as needed.

![Add Ingress Rule pane](<../../../.gitbook/assets/image (57) (2).png>)

{% hint style="info" %}
DuploCloud Platform supports defining multiple paths in Ingress.
{% endhint %}

Continuing our previous example, we have defined an Ingress to route requests to `/path1/`for **testsvc1**, and requests to `/path2/` for **testsvc2**. For the third service, we have brought out own host (BYOH), **example.com**. In this example, the Ingress rules apply only to **example.com**.

![Kubernetes Ingress rules](<../../../.gitbook/assets/image (13).png>)

## Add Load Balancer with Kubernetes NodePort

Add a load balancer listener that uses Kubernetes NodePort.

{% hint style="info" %}
Using Kubernetes Health Check allows AWS's Application Load Balancer to determine whether your service is running properly.&#x20;
{% endhint %}

1. In the DuploCloud Portal, navigate **DevOps** -> **Containers -> EKS/Native**.
2. On the Services page, select the Service name in the **Name** column.
3. Click the **Load Balancers** tab.
4. Click **Configure Load Balancer**. The **Add Load Balancer Listener** pane appears.
5. In the **Select Type** field, select **K8S Node Port**.&#x20;
6. Optionally, select **Set Health Check annotations for Ingress** to add Kubernetes Health Checks and Probes.&#x20;
7. Complete the other fields in the **Add Load Balancer Listener** and click **Add**.

## View Ingress

Once Ingress is configured, you can access Services based on the rules for each **DNS**.

![K8s Ingress Tab](<../../../.gitbook/assets/image (18) (5).png>)

By executing `curl` commands, you can see the difference in the output for each service. Configured services are accessed based on the DNS name specified in the DuploCloud Portal and the paths that you configured when you added Ingress rules.

> `>curl http://sample-ingress.qaapps.duplocloud.net/path1/` \
> `this is service1`\
> \
> `>curl http://sample-ingress.qaapps.duplocloud.net/path2/` \
> `this is service2`\
> \
> `>curl -H "Host: example.com" http://sample-ingress.qaapps.duplocloud.net/ this is service3`

