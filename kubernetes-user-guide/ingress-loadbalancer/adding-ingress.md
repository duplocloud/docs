---
description: Set up Kubernetes Ingress and Load Balancer with K8s NodePort
---

# EKS Ingress

## Creating a Kubernetes Ingress and Load Balancer

Ingress controllers abstract the complexity of routed Kubernetes application traffic, providing a bridge between Kubernetes services and services that you define.

### Creating Tenants, Hosts, and Services with EKS

See the [Containers ](../../aws/aws-services/containers/)topic for steps on how to create [Tenants](../../getting-started/application-focussed-interface/tenant.md), Hosts, and [Services](../../getting-started/application-focussed-interface/app-service-and-cloud-services.md).

Once your service is deployed, you are ready to add and configure Kubernetes Ingress by [enabling the AWS Application Load Balancer](adding-ingress.md#enabling-the-aws-application-load-balancer).

### Enabling the AWS Application Load Balancer&#x20;

Your administrator needs to enable the AWS Application Load Balancer controller for your infrastructure before you can use Ingress.

1. In the DuploCloud Portal, navigate to **Administrator ->** **Infrastructure** and select the Infrastructure name from the **NAME** column. Select the **Settings** tab.
2. Click **Add**. The **Infra - Custom Data** pane displays.
3. From the **Setting Name** list box, select **Enable ALB Ingress Controller**.
4. Select **Enable**.
5. Click **Set**. In the Settings tab, the **Enable ALB Ingress Controller** setting displays a **Value** of **true**.&#x20;

<figure><img src="../../.gitbook/assets/k8aws10.png" alt=""><figcaption><p><strong>Settings</strong> tab on the <strong>Infrastructure</strong> page</p></figcaption></figure>

### Adding a Load Balancer with Kubernetes NodePort

Add a load balancer listener that uses Kubernetes (K8s) NodePort. Kubernetes Health Check and Probes are enabled by default. To specifically configure the settings for Health Check, select **Additional Health Check configs** when you add the Load Balancer.

1. In the DuploCloud Portal, navigate **Kubernetes** -> **Services**.
2. On the **Services** page, select the Service name in the **Name** column.
3. Click the **Load Balancers** tab.
4.  Click **Configure Load Balancer**. The **Add Load Balancer Listener** pane appears.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/k8aws.png" alt=""><figcaption><p><strong>Add Load Balancer LIstener</strong> pane</p></figcaption></figure>

    </div>


5. In the **Select Type** field, select **K8S Node Port**.&#x20;
6. Complete the other required fields in the **Add Load Balancer Listener** pane and click **Add**. The Load Balancer displays in the **Load Balancers** tab.

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.16-14_44_43.png" alt=""><figcaption><p><strong>Load Balancers</strong> tab for <strong>filebeat-k8s-duploinfrasvc</strong></p></figcaption></figure>

### Add Kubernetes Ingress

Once Services are deployed, add Ingress:

1. From the DuploCloud portal, navigate to **Kubernetes** -> **Ingress**.&#x20;
2. Click **Add**. The **Add Kubernetes Ingress** page displays.

{% hint style="warning" %}
You must define [rules ](https://kubernetes.io/docs/concepts/services-networking/ingress/#ingress-rules)to add a Kuberenetes Ingress. [Continue to the next section to add rules](adding-ingress.md#add-rules-to-kubernetes-ingress-and-complete-ingress-setup) to Kubernetes Ingress and complete the Ingress setup.&#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.16-14_50_26.png" alt=""><figcaption><p><strong>Add Kubernetes Ingress</strong> page with highlighted <strong>Add Rule</strong> option</p></figcaption></figure>

### Add rules to Kubernetes Ingress and complete Ingress setup

1.  In the **Add Kubernetes Ingress** page, configure Ingress by clicking **Add Rule**. The **Add Ingress Rule pane** displays. \


    <div align="left">

    <img src="../../.gitbook/assets/k8aws7.png" alt="Add Ingress Rule pane">

    </div>


2. Specify the **Path** (**/path1/** in the example above).
3. From the **Service Name** list box, select the Service exposed through the K8S Node Port (**js-service1** in the example above). The **Container port** field is completed automatically.&#x20;
4. Optionally, complete **Path Type** and **Host**. In this example, we specify a **Path Type** of **Exact**. Clicking the Info Tip icon ( <img src="../../.gitbook/assets/info_tip_black (1).png" alt="" data-size="line"> ) provides more information for these optional fields.
5. Click **Add Rule**. The rule is displayed on the **Add Kubernetes Ingress** page. Add additional rules by repeating the preceding steps.

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.16-14_53_23.png" alt=""><figcaption><p><strong>Add Kubernetes Ingress</strong> page</p></figcaption></figure>

6. On the **Add Kubernetes Ingress** page, specify the **Ingress Name**.
7. From the **Ingress Controller** list box, select the [Ingress Controller that you defined previously](adding-ingress.md#enabling-the-aws-application-load-balancer).
8. From the **Visibility** list box, select either **Internal Only** or **Public**.&#x20;
9. From the **Certificate ARN** list box, select the appropriate ARN.
10. Click **Add** to add the Kubernetes Ingress with defined rules. The Ingress you added displays in the **K8S Ingress** tab.\


    <figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.16-14_57_51.png" alt=""><figcaption><p> <strong>The Ingress</strong> page displaying the added Ingress</p></figcaption></figure>


11. DuploCloud Platform supports defining multiple paths in Ingress. We defined an Ingress rule with an **Exact Path Type** to route requests to `/path1/`for **js-service1**. To continue this example, we added a rule with a **Prefix Path Type** to route requests to `/path2/` for **testsvc2.** Additionally, we added a rule with a **Prefix Path Type** to route requests via a [BYOH Host](../../extras/byoh.md) (Bring-Your-Own-Host) named **example.com**, for a third service, **testsvc3**.

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.16-15_02_12.png" alt=""><figcaption><p>Multiple paths defined for an <strong>Ingress</strong> in the DuploCloud Portal</p></figcaption></figure>

## Viewing Ingress

When Ingress is configured, you can access Services based on the rules for each **DNS**, displayed on the **Kubernetes** -> **Ingress** page.&#x20;

In this example, we display the output for three services with **Path Type** rules and different DNS names. See the [previous example](adding-ingress.md#add-rules-to-kubernetes-ingress-and-complete-ingress-setup) for detailed steps to create Ingress rules.



<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.16-15_06_22.png" alt=""><figcaption><p> <strong>Ingress</strong> page with multiple Ingresses for specific DNS names.</p></figcaption></figure>

By executing `curl` commands, you can see the difference in the output for each service in this example. Configured services are accessed based on the DNS name specified in the DuploCloud Portal and the paths that you specified when you added Ingress rules.

> `>curl http://ig-nev-ingress-ing-t2-1-duplopoc.net/`_`path-x`_`/`\
> `this is service1`\
> \
> `>curl http://ing-doc-ingress-ing-t2-1-duplopoc.net/`_`path-y`_`/`\
> `this is service2`
>
> \
> `>curl http://ing-public-ingress-ing-t2.1.duplopoc.net/`_`path-z`_`/`
>
> `this is ING2-PUBLIC`

