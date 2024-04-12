---
description: Create a GKE Ingress using the DuploCloud Portal
---

# GKE Ingress

## Creating a GKE Ingress Controller

GCP's Ingress Controller for GKE automatically manages traffic routing to Kubernetes services, integrating Kubernetes workloads with Google Cloud's load-balancing infrastructure. It simplifies external access to applications, handling SSL termination and global load distribution.

GCP offers its own Ingress Controller, specifically created for Google Kubernetes Engine (GKE), to seamlessly integrate Kubernetes services with Google Cloud's advanced load balancing features.

### Container Native Load Balancing with GKE Ingress

Container-native load balancing on Google Cloud Platform (GCP) allows load balancers to directly target Kubernetes Pods instead of using a node-based proxy. This approach improves performance by enabling more efficient routing, reducing latency by eliminating extra hops and providing better health-checking capabilities.&#x20;

It leverages the network endpoint groups (NEGs) feature to ensure that traffic is directed to the appropriate container instances, enabling more granular and efficient load distribution for applications running on GKE.

<figure><img src="../../.gitbook/assets/image (121).png" alt="" width="563"><figcaption><p><strong>GKE Container Native Load Balancing</strong></p></figcaption></figure>

## Prerequisites

### Creating Tenants and Services

See the [Containers ](../../aws-user-guide/aws-services/containers/)topic for steps on how to create [Tenants](../../getting-started/application-focussed-interface/tenant/), and [Services](../../getting-started/application-focussed-interface/app-service-and-cloud-services.md).

Once your services are deployed, you are ready to add and configure a GKE Ingress controller in GCP.

### Adding a Duplo LoadBalancer listener with Kubernetes ClusterIP

Add a load balancer listener that uses Kubernetes (K8s) ClusterIP type service. Kubernetes Health Check and Probes are enabled by default. To specifically configure the settings for Health Check, select **Additional Health Check configs** when you add the Load Balancer.

1. In the DuploCloud Portal, navigate **Kubernetes** -> **Services.**
2. On the **Services** page, select the Service name in the **Name** column.
3. Click the **Load Balancers** tab.
4. Click **Configure Load Balancer**. The **Add Load Balancer Listener** pane appears.

<div align="left">

<figure><img src="../../.gitbook/assets/image (122).png" alt="" width="375"><figcaption><p><strong>Add Load Balancer Listener</strong> pane</p></figcaption></figure>

</div>

5. From the **Select Type** list box, select **K8S Cluster IP**.&#x20;
6. Complete the other required fields in the **Add Load Balancer Listener** pane and click **Add**. The Load Balancer displays in the **Load Balancers** tab.
7. Click **Advanced Kubernetes Settings** and enable **Set Health Check annotations for Ingress.** (This will add required annotations in Kubernetes Service to be recognized by the GKE Ingress Controller)
8. Click **Add.**

<figure><img src="../../.gitbook/assets/image (123).png" alt=""><figcaption><p><strong>Load Balancers</strong> tab for <strong>nginx-test</strong> service</p></figcaption></figure>

### Create a GCP Managed Certificate (optional)

In order to enable SSL, you can create a GCP-managed certificate resource in the application namespace.

```
apiVersion: networking.gke.io/v1
kind: ManagedCertificate
metadata:
  name: my-managed-cert
  namespace: duploservices-npdev04gke
spec:
  domains:
  - npdev04.duplocloud.net #your A record name in DNS
```

## Add a Kubernetes Ingress

Once Services are deployed, add an Ingress:

1. Select **Kubernetes** -> **Ingress** from the navigation pane.
2. Click **Add**. The **Add Kubernetes Ingress** page displays.

{% hint style="warning" %}
You must define [rules ](https://kubernetes.io/docs/concepts/services-networking/ingress/#ingress-rules)to add a Kubernetes Ingress. [Continue to the next section to add rules](gke-ingress.md#add-rules-to-kubernetes-ingress-and-complete-ingress-setup) to Kubernetes Ingress and complete the Ingress setup.&#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/image (124).png" alt=""><figcaption><p><strong>Add Kubernetes Ingress</strong> page with highlighted <strong>Add Rule</strong> option</p></figcaption></figure>

### Add rules to Kubernetes Ingress and complete Ingress setup

1. In the **Add Kubernetes Ingress** page, configure Ingress by clicking **Add Rule**. The **Add Ingress Rule pane** displays.&#x20;

<div align="left">

<figure><img src="../../.gitbook/assets/image (125).png" alt="" width="375"><figcaption><p><strong>Add Ingress Rule</strong> pane</p></figcaption></figure>

</div>

2. Specify the **Path** (**/samplePath/** in the example above).
3. From the **Service Name** list box, select the Service exposed through the K8S ClusterIP (**nginx-test** in the example above). The **Container port** field is completed automatically.&#x20;
4. Optionally, complete **Path Type** and **Host**. In this example, we specify a **Path Type** of **Exact**. Clicking the Info Tip icon ( <img src="../../.gitbook/assets/info_tip_black (1).png" alt="" data-size="line"> ) provides more information for these optional fields.
5. Click **Add Rule**. The rule is displayed on the **Add Kubernetes Ingress** page. Add additional rules by repeating the preceding steps.

<figure><img src="../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

6. On the **Add Kubernetes Ingress** page, specify the **Ingress Name**.
7. From the **Ingress Controller** list box, select **gce.**
8. From the **Visibility** list box, select **Internal Only** or **Public**.&#x20;
9. If you have [created a GCP managed cert](gke-ingress.md#create-gcp-managed-certificate-optional)[ificate](gke-ingress.md#create-a-gcp-managed-certificate-optional), add the following annotations in the **Annotations** field to link the Ingress with your GCP managed certificate

```
"networking.gke.io/managed-certificates" = "my-managed-cert",
"kubernetes.io/ingress.allow-http" = "false"
```

10. Click **Add** to add the Kubernetes Ingress with defined rules. The Ingress you added displays in the **Ingress** page.

<figure><img src="../../.gitbook/assets/image (127).png" alt=""><figcaption><p><strong>Ingress</strong> page displaying added Ingress</p></figcaption></figure>

## Viewing Ingress

When Ingress is configured, you can access Services based on the rules for each **DNS**, displayed in the **K8S Ingress** tab.&#x20;

In this example, we display the output for three Services with **Path Type** rules and different DNS names. See the [previous example](gke-ingress.md#add-rules-to-kubernetes-ingress-and-complete-ingress-setup) for detailed steps to create Ingress rules.

<figure><img src="../../.gitbook/assets/image (128).png" alt=""><figcaption><p><strong>K8s Ingress</strong> Tab for specific DNS names</p></figcaption></figure>

The Ingress creation will take a few minutes. Once the IP is attached to the ingress, you are ready to use your path- or host-based routing defined via ingress!
