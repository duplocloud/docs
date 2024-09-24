---
description: Enable shell access for native Docker or ECS users
---

# Shell Access for Docker or ECS

DuploCloud allows shell access into the deployed containers. Shell access is enabled differently, depending on whether you use native Docker or ECS.

## Enabling Secure Shell (SSH) Access for Docker Containers

1. In the DuploCloud Portal, navigate to **Docker** -> **Services**.&#x20;
2. From the **Docker** list box, select **Enable Docker Shell**. The **Start Shell Service** pane displays.

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.17-14_19_17.png" alt=""><figcaption><p>The <strong>Enable Docker Shell</strong> option in the <strong>Options</strong> menu on the <strong>Services</strong> page</p></figcaption></figure>

<div align="left">

<figure><img src="../../.gitbook/assets/Screenshot 2024-09-24 at 12.17.53 PM.png" alt=""><figcaption><p>The <strong>Start Shell Service</strong> pane</p></figcaption></figure>

</div>

3. From the **Certificate** list box, select your certificate.
4. From the **Visibility** list box, select **Public** or **Internal**.&#x20;
5. Click **Update**. A provisioned Service named **dockerservices-shell** is created, enabling you to access containers using SSH.

## Accessing the Task Shell for ECS

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **ECS**. The **ECS** **Task Definition** page displays.
2. Select the name from the **TASK DEFINITION FAMILY NAME** column.
3. Select the **Tasks** tab.
4. To display the ECS task shell for any task, click on the **(>\_**) icon in the **Actions** column of the appropriate row. Click on the container task shell option. A browser launches, giving access to the shell.

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.17-14_36_14.png" alt=""><figcaption><p>The <strong>ECS task shell</strong> option in the menu of the <strong>Tasks</strong> tab</p></figcaption></figure>

## Enabling a Kubernetes shell

1. In the **Tenant** list box, select the **Default** Tenant.
2. In the DuploCloud portal, navigate to **Docker** -> **Services**.
3. Click the **Docker** button on the upper right, and select **Enable Docker Shell**. The **Start Shell Service** pane displays.

<div align="left">

<figure><img src="../../.gitbook/assets/shell service123 (1).png" alt=""><figcaption><p>The <strong>Start Shell Service</strong> pane</p></figcaption></figure>

</div>

4. In the **Platform** list box, select **Kubernetes**.
5. Select the appropriate certificate from the **Certificate** list box.
6. In the **Visibility** list box, select **Public**.
7. Click **Update**. DuploCloud provisions the **dockerservices-shell** service, enabling you to access your Docker containers using the Kubernetes shell.

Once the service is provisioned, you can access the Kubernetes shell by navigating to **Kubernetes** -> **Services** in the DuploCloud portal and clicking the **KubeCtl Shell** button. This will launch the Kubernetes shell, allowing you to interact with your Docker containers running on the Kubernetes platform.
