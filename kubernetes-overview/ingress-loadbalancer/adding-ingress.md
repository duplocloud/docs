---
description: Adding an Ingress for DuploCloud Amazon Web Services Load Balancers
---

# EKS Ingress

Ingress controllers abstract the complexity of routed Kubernetes application traffic, providing a bridge between Kubernetes services and services that you define.

## Prerequisites

### Creating Tenants, Hosts, and Services with EKS

See the DuploCloud documentation for steps on how to create [Tenants](https://docs.duplocloud.com/docs/overview/use-cases/tenant-environment), [Hosts](https://docs.duplocloud.com/docs/overview/use-cases/hosts-vms/adding-hosts), and [Services](../../welcome-to-duplocloud/application-focussed-interface/app-service-and-cloud-services.md)[.](https://docs.duplocloud.com/docs/overview/aws-services/containers/eks-containers-and-services)

Once your Service(s) are deployed, you can [enable the AWS Load Balancer](adding-ingress.md#enabling-the-aws-application-load-balancer).

### Enabling the AWS Application Load Balancer&#x20;

An administrator needs to enable the AWS Application Load Balancer controller for your Infrastructure before you can use Ingress.

1. In the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure** and select the Infrastructure name from the **NAME** column. Select the **Settings** tab.
2. Click **Add**. The **Infra - Custom Data** pane displays.
3. From the **Setting Name** list box, select **Enable ALB Ingress Controller**.
4. Select **Enable**.
5. Click **Set**. In the **Settings** tab, the **Enable ALB Ingress Controller** displays a value of **true**.&#x20;

<figure><img src="../../.gitbook/assets/k8aws10.png" alt=""><figcaption><p><strong>Settings</strong> tab on the <strong>Infrastructure</strong> page</p></figcaption></figure>

### Adding a Load Balancer with Kubernetes NodePort

Add a Load Balancer listener that uses Kubernetes NodePort. Kubernetes Health Check and Probes are enabled by default. To specifically configure the settings for Health Check, select **Additional health check configs** when you add the Load Balancer.

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Services**.
2. On the **Services** page, select the Service name.
3. Click the **Load Balancers** tab.
4.  Click **Configure Load Balancer**. The **Add Load Balancer Listener** pane appears.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/k8aws.png" alt=""><figcaption><p><strong>Add Load Balancer LIstener</strong> pane</p></figcaption></figure>

    </div>


5. In the **Select Type** field, select **K8S Node Port**.&#x20;
6. Complete the other required fields in the **Add Load Balancer Listener** pane and click **Add**. The Load Balancer displays on the **Service** page in the **Load Balancers** tab.

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.16-14_44_43.png" alt=""><figcaption><p><strong>Load Balancers</strong> tab for <strong>filebeat-k8s-duploinfrasvc</strong></p></figcaption></figure>

## Adding a Kubernetes Ingress

Once Services and Load Balancers are deployed, add an Ingress:

1. From the DuploCloud Portal, navigate to **Kubernetes** -> **Ingress**.
2. Click **Add**. The **Add Kubernetes Ingress** page displays.
3. On the **Add Kubernetes Ingress** page, specify the **Ingress Name**.
4. From the **Ingress Controller** list box, select the [Ingress Controller that you defined previously](adding-ingress.md#enabling-the-aws-application-load-balancer).
5. From the **Visibility** list box, select either **Internal Only** or **Public**.&#x20;
6. From the **Certificate ARN** list box, select the appropriate ARN.
7. Enter port numbers in the **HTTP Listener Port** and **HTTPS Listener Port** fields, if needed. \


<figure><img src="../../.gitbook/assets/ingress new.png" alt=""><figcaption><p>The <strong>Add Kubernetes Ingress</strong> page.</p></figcaption></figure>

{% hint style="warning" %}
To add a Kubernetes Ingress, you must define rules. Continue to the next section to add Kubernetes Ingress rules and complete the setup.&#x20;
{% endhint %}

### Configuring Kubernetes Ingress rules

1. On the **Add Kubernetes Ingress** page, configure an Ingress rule by clicking **Add Rule**. The **Add Ingress Rule pane** displays.&#x20;

<div align="left">

<figure><img src="../../.gitbook/assets/Add Ingress Rule.png" alt=""><figcaption><p>The <strong>Add Ingress Rule</strong> pane.</p></figcaption></figure>

</div>

2. Specify the **Path** (**/** in the example above).
3. To use a container port name (optional), use the toggle switch to enable **Use Container Port Name**.
4. If you enabled **Use Container Port Name** in Step 3., type a Service name in the Service Name field (**redirect:use-annotation** in the example) and a container port name in the **Container Port** field (**use-annotation** in the example). &#x20;
5. If you did not enable **Use Container Port Name** in Step 3., select the Service exposed through the K8S Node Port from the **Service Name** list box. The **Container Port** field is completed automatically.
6. Optionally, specify the **Path Type** and **Host**. In this example, we specify a **Path Type** of **Exact**. Clicking the Info Tip icon ( <img src="../../.gitbook/assets/info_tip_black (1).png" alt="" data-size="line"> ) provides more information for these optional fields.
7.  Click **Add Rule**. The rule is displayed on the **Add Kubernetes Ingress** page. Repeat the preceding steps to add additional rules.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.03.04-15_57_54.png" alt=""><figcaption><p>The <strong>Add Ingress</strong> page</p></figcaption></figure>

    </div>



{% hint style="info" %}
DuploCloud Platform supports defining multiple paths in Ingress. As shown in the following example, you could add one Ingress rule with path type **Exact** to route requests to `/path1/`for **js-service1**, add a second rule with path type **Prefix** to route requests to `/path2/` for **testsvc2**, and add a third rule with path type **Prefix** to route requests via a [BYOH Host](../../extras-overview/byoh.md) (Bring-Your-Own-Host) named **example.com** for a third service, **testsvc3**.
{% endhint %}

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.16-15_02_12.png" alt=""><figcaption><p>Multiple paths defined for an <strong>Ingress</strong> in the DuploCloud Portal</p></figcaption></figure>

### Adding Ingress redirect config and annotations

1.  On the **Add Kubernetes Ingress** page, click **Add Redirect Config**. The **Add Redirect Config** pane displays.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/redirect config.png" alt=""><figcaption><p>The <strong>Add Redirect Config</strong> pane</p></figcaption></figure>

    </div>
2. Fill in the necessary fields.&#x20;
3.  Click **Add** to add the Kubernetes Ingress. The Ingress you added displays in the **K8S Ingress** tab.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.16-14_57_51.png" alt=""><figcaption><p> <strong>The Ingress</strong> page displaying the added Ingress</p></figcaption></figure>

    </div>



## Viewing Ingress

When Ingress is configured, you can access Services based on the rules for each **DNS** displayed on the **Kubernetes** -> **Ingress** page.&#x20;

In this example, we display the output for three Services with path type rules and different DNS names. See the [detailed steps to create Ingress rules](adding-ingress.md#configuring-kubernetes-ingress-rules).

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.16-15_06_22.png" alt=""><figcaption><p> <strong>Ingress</strong> page with multiple Ingresses for specific DNS names.</p></figcaption></figure>

By executing `curl` commands, you can see the difference in the output for each Service in this example. Configured Services are accessed based on the DNS name specified in the DuploCloud Portal and the paths you specified when adding Ingress rules.

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

