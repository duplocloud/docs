---
description: Creating a Load Balancer to configure network ports to access the application
---

# Step 5: Create a Load Balancer

Now that your DuploCloud Service is running, you have a mechanism to expose the containers and images in which your application resides. But because your containers are running inside a private network, you also need a load balancer to listen on the correct ports to access the application.

In this step, we add a Load Balancer Listener to complete this network configuration.

_Estimated time to complete Step 5: 10 minutes._

## Prerequisites

Before creating a Load Balancer, verify that you accomplished the tasks in the previous tutorial steps.   Using the DuploCloud Portal, confirm that:

* An [Infrastructure and Plan](../step-1-infrastructure.md) exist, both with the name you created.
* The Infrastructure you created has [GKE Enabled](../step-1-infrastructure.md).
* A [Tenant](../../../overview-2/quick-start/step-2-tenant.md) with the name you chose has been created.
* A [Node Pool](../../use-cases/creating-an-infrastructure-and-plan-for-gcp/creating-gke-standard-service.md) had been created.
* A [Service](../create-a-service-with-gke-autopilot/step-3-create-app-via-k8s.md) with the name you chose has been created.&#x20;

### Select the Tenant you created

In the **Tenant** list box, on the upper-left side of the DuploCloud Portal, select the Tenant that you created.

## Creating a Load Balancer

All containers are running inside a private network and cannot be accessed from an external network. To allow external access, create a Load Balancer:

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Services**. The **Services** page displays.&#x20;
2. From the **NAME** column, select the name of your **Service**
3. Click the **Load Balancers** tab.
4. Click the **Configure Load Balancer** link. The **Add Load Balancer Listener** pane displays.

<div align="left"><figure><img src="../../../.gitbook/assets/image (82).png" alt=""><figcaption><p><strong>Add Load Balancer Listener</strong> pane</p></figcaption></figure></div>

5. From the **Type** list box, select **Application LB**.
6. In the **Container Port** field, enter **80**. This is the configured port on which the application inside the Docker Container Image is running.&#x20;
7. In the **External Port** field, enter **80**. This is the port through which users will access the web application.
8. From the **Visibility** list box, select **Public**.
9. From the **Application Mode** list box, select **Docker Mode**.
10. Type **/** (forward-slash) in the **Health Check** field to indicate that the cluster we want Kubernetes to perform Health Checks on is located at the `root` level.
11. In the **Backend Protocol** list box, select **HTTP**. HTTP is used for this tutorial since we are not setting up SSL certificates. However, using HTTPS to encrypt data between the user and the server when configuring Load Balancers is highly recommended. If you decide to use HTTPS, you must [configure SSL certificates](../../prerequisites/certificate-for-load-balancer-and-ingress.md).
12. **Certificates:** You can leave this field empty, as SSL certificates are not necessary for this tutorial. However, we recommend using SSL certificates with Load Balancers to ensure secure HTTPS connections. If you'd like to add SSL certificates for your domain later, follow the instructions [here](../../prerequisites/certificate-for-load-balancer-and-ingress.md).
13. Click **Add**. The Load Balancer is created and initialized. In approximately 2-3 minutes you will see the load balancer details available in the portal. The **LB Status** card displays **Ready** when the Load Balancer is ready.&#x20;

## Checking your work

1. From the DuploCloud portal, navigate to **Kubernetes** -> **Services**.
2. Click on the name of your **Service**.
3. Verify that the **LB Status** card displays a status of **Ready**

<figure><img src="../../../.gitbook/assets/Screenshot (213).png" alt=""><figcaption><p><strong>Services</strong> details page showing a <strong>LB Status</strong> of <strong>Ready</strong></p></figcaption></figure>
