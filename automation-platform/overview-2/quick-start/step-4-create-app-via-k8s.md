---
description: Create a DuploCloud Service for application deployment
---

# Step 4: Create a Service

With all of the core components of your DuploCloud platform configured, enabled, and running, you're ready to deploy applications with Azure, using AKS and Kubernetes.

In order to deploy applications, you must first create a DuploCloud Service to connect to the Docker containers and images where your application code exists. Once you create a Service from the DuploCloud Portal, you can also perform tasks that you might perform when working with a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/). For example, you can view container logs, container state, and container shell, as well as get access to `kubectl`, which allows you to work directly with Kubernetes constructs such as Pods.

In this step, we create a Service to connect a [Docker](https://www.docker.com/) that displays a simple Welcome message on a web page.&#x20;

_Estimated time to complete Step 4: 15 minutes._

{% hint style="info" %}
See the Docker documentation for an [overview of containers and images](https://docs.docker.com/get-started/).
{% endhint %}

## Prerequisites

Before creating your DuploCloud Service, ensure that:

* All previous steps in this tutorial to create an [Infrastructure and Plan](step-1-infrastructure.md), [Tenant](step-2-tenant.md), [Host, and Azure Agent Pool](step-3-create-azure-agent-pool.md) are complete.
* The [AKS Kubernetes cluster](step-1-infrastructure.md#enabling-the-aks-kubernetes-cluster) is enabled.
* Tenant **DEV01** is selected in the **Tenant** list box, at the top of the DuploCloud Portal.

<div align="left"><figure><img src="../../../.gitbook/assets/tenant_dev01 (6).png" alt=""><figcaption><p><strong>Tenant</strong> list box with Tenant <strong>DEV01</strong> selected</p></figcaption></figure></div>

## Creating a Service

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Services**.
2.  Click **Add**. The **Add Service** page displays.\


    <div align="left"><img src="../../../.gitbook/assets/image (301).png" alt="Add Service page to add nginx-service"></div>
3. In the **Service Name** field, enter `nginx-service`.
4. Specify the Docker image that you use to run the application. In the Docker Image field, enter `nginx:latest`.&#x20;
5. Click **Next**, accepting all other defaults. The **Advanced Options** page displays.
6. Scroll down if needed and click **Create**.

## Checking Your Work

The Service may take a few minutes to start up. Before moving on to the next step, navigate to the **Services** page (**Kubernetes** -> **Services**), click on the name of the **Service**, and verify that the status is **Running**.

<figure><img src="../../../.gitbook/assets/Screenshot (354).png" alt=""><figcaption><p>The <strong>Service</strong> details page</p></figcaption></figure>
