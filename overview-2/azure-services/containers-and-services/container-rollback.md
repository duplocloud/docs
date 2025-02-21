---
description: Roll back a container image for Kubernetes or Docker Services
---

# Container Rollback

Container Rollback in DuploCloud allows users to quickly revert a Kubernetes or Docker Service's container image to a previous, stable version. This is especially useful in scenarios where a newly deployed container image introduces issues, errors, or failures in the application. With this feature, users can ensure minimal downtime and maintain the stability of their Services by rolling back to a known good state. Container rollback is support for:

* **Kubernetes** (on EKS, AKS, GKE, and DuploCloud Kubernetes)
* **Docker Services** (on ECS)

## Rolling back a container image

To roll back a container image in DuploCloud for your GKE Service, first configure system settings to enable container history tracking, and then roll back the container image:

### **Configuring system settings to enable container image history tracking**

1. Navigate to **Admin** -> **System Settings**.
2. Select the **System Config** tab and click **Add** to create a new configuration.
3. For **Config Type**, select **Flags**.
4. In the **Flag Name** field, choose **Enable Container Image History Tracking**.
5. Set the **Value** to **True** and click **Submit**.

<figure><img src="../../../.gitbook/assets/system config (1).png" alt=""><figcaption><p>The <strong>System Config</strong> page in the DuploCloud Portal</p></figcaption></figure>

### Rolling back a container image

1. Select the appropriate Tenant from the **Tenant** list box.
2. Navigate to **Kubernetes** -> **Services** or **Docker** -> **Services**.
3. In the **NAME** column, select the service you want to roll back.
4.  From the **Actions** menu, choose **Rollback**. The **Rollback Container Image** pane will appear.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (48).png" alt="" width="363"><figcaption></figcaption></figure></div>
5. In the **Image** list box, select the version of the container image you want to roll back to.
6. Click **Rollback** to revert the service to the selected image.
