---
description: Creating a Kubernetes Service to run a Docker-containerized application
---

# Step 4: Create a Service

In this exercise, we will create a simple Google Cloud Nginx service. When you run the application, DuploCloud accesses Docker images in a preconfigured Docker Hub.&#x20;

When you run your own applications, you will choose a public image or provide credentials to access your private repository. Before you deploy your own applications, [configure your Docker Registry credentials in DuploCloud](../../../overview/aws-services/containers/docker-registry-credentials.md).

_Estimated time to complete Step 4: 10 minutes._

## Prerequisites

Before creating a Service, verify that you accomplished the tasks in the previous tutorial steps. Using the DuploCloud Portal, confirm that:

* An [Infrastructure and Plan](../step-1-infrastructure.md) exist, both with the name that you chose.
* The Infrastructure has [GKE **Enabled**](../step-1-infrastructure.md).
* A [Tenant](../step-2-tenant.md) with the name you chose has been created.
* A [Node Pool ](step-3-create-a-node-pool.md)had been created.

### Select the Tenant you created

In the **Tenant** list box, on the upper-left side of the DuploCloud Portal, select the Tenant that you created.

## Adding a Service

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Services**. The **Services** page displays.&#x20;
2. Click **Add**. The **Add Service** page displays.
3. In the **Service** **Name** field, enter a name for the service (in the example below, the name is "myservice").
4. In the **Docker image** field, enter `nginx:latest`.

<figure><img src="../../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.23-14_16_57.png" alt=""><figcaption><p>The Kubernetes, <strong>Add Service</strong> page.</p></figcaption></figure>

5. Click **Next**. The **Advanced Options** page is displayed.
6. At the bottom of the **Advanced Options** page, click **Create**. Your Service is created and initialized.&#x20;

{% hint style="info" %}
It may take approximately five (5) minutes for the Service to initialize. Use the **Containers** page (**Kubernetes** -> **Containers**) to monitor the Service creation status, between **Desired** (**Running**) and **Current**.&#x20;
{% endhint %}

## Checking your work

From the DuploCloud portal, navigate to **Kubernetes** -> **Services**, and verify that your DuploCloud Service has a **Current** status of **Running**.

<figure><img src="../../../.gitbook/assets/screenshot-nimbusweb.me-2024.03.04-19_28_55.png" alt=""><figcaption><p>The <strong>Services</strong> page showing the running Service</p></figcaption></figure>

