---
description: Roll back a container image for Kubernetes or Docker Services
---

# Container Rollback

Container Rollback in DuploCloud allows users to quickly revert a Kubernetes or Docker Service's container image to a previous, stable version. This is especially useful in scenarios where a newly deployed container image introduces issues, errors, or failures in the application. With this feature, users can ensure minimal downtime and maintain the stability of their Services by rolling back to a known good state. Container rollback is support for:

* **Kubernetes** (on EKS, AKS, GKE, and DuploCloud Kubernetes)
* **Docker Services**

## Rolling back a container image

1. Select the appropriate Tenant from the **Tenant** list box.
2. Navigate to **Kubernetes** -> **Services** or **Docker** -> **Services**.
3. In the **NAME** column, select the service you want to roll back.
4.  From the **Actions** menu, choose **Rollback**. The **Rollback Container Image** pane will appear.<br>

    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (48).png" alt="" width="363"><figcaption></figcaption></figure></div>
5. In the **Image** list box, select the version of the container image you want to roll back to.
6. Click **Rollback** to revert the service to the selected image.

## **Disabling container image history tracking**

1. Navigate to **Admin -> System Settings**.
2. Select the **System Config** tab and click **Add**. The **Add Config** pane displays.&#x20;
3. For **Config Type**, select **Flags**.
4. In the **Key** list box, select **Disable Container Image History Tracking**.
5. Set the **Value** to **True** to disable image history tracking (default is **False**).
6. Click **Submit**. The setting is saved.

<figure><img src="../../../../.gitbook/assets/system config (2).png" alt=""><figcaption><p>The <strong>Add Config</strong> pane configured to disable container image history tracking</p></figcaption></figure>
