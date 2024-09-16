---
description: Enable shell access for native Docker or ECS users
---

# Shell Access for Docker or ECS

DuploCloud allows shell access into the deployed containers. Shell access is enabled differently, depending on whether you use native Docker or ECS.

## Enabling Secure Shell (SSH) Access for Docker Containers

1. In the DuploCloud Portal, navigate to **Docker** -> **Services**. The **Services** page displays.
2. From the **Docker** list box, select **Enable Docker Shell**. The **Start Shell Service** pane displays.

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.17-14_19_17.png" alt=""><figcaption><p>The <strong>Enable Docker Shell</strong> option in the <strong>Options</strong> menu on the <strong>Services</strong> page</p></figcaption></figure>

<div align="left">

<figure><img src="../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.17-14_22_46.png" alt=""><figcaption><p>The <strong>Start Shell Service</strong> pane</p></figcaption></figure>

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
