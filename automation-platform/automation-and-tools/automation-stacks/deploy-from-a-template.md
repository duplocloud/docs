---
description: Deploy resources to Tenants using templates with DuploCloud Stacks
---

# Deploy from a template

Deploy resources (Nodes, Hosts, Services, Secrets, storage, etc.) to a Tenant using the DuploCloud Stacks feature.&#x20;

## Uploading templates

Upload templates in advance to make them available for deployment across all Tenants or for a specific Tenant to make them available only within that Tenant's environment. You can upload a template for a specific Tenant ahead of time, or at the time of deployment.

### Uploading a template for all Tenants

1. From the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Select the **Templates** tab.
3.  Click **Upload**. The **Upload Template** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/upload template pane (1).png" alt="" width="374"><figcaption><p>The <strong>Upload Template</strong> pane</p></figcaption></figure></div>
4. Enter a name for the template in the **File Name** field.
5. In the **Module Type** list box, **Stack** is selected by default. For steps related to the **Agent** Module Type, see below.
6. Click **Choose File** and select the file to upload.
7. Click **Upload**.

### Uploading a template for a specific Tenant

1. Select the Tenant that will use the template from the **Tenant** list box.
2. Navigate to **Automation** -> **Stacks**.
3. Select the **Templates** tab, and click **Upload**. The **Upload Template** pane displays.
4. Enter a name for the template in the **Name** field.
5. Click **Choose File**, and select the file to upload.
6. Click **Upload**.

### Uploading a template during deployment

While creating a deployment following the [steps below](deploy-from-a-template.md#deploying-a-stack-template), select the **Upload File** option, and upload the template you wish to use for the deployment.&#x20;

## Viewing a template

Access a read-only version of the template to view. To download an editable version of a template, see the [instructions below](deploy-from-a-template.md#downloading-a-template).&#x20;

### Viewing a template available to all Tenants

1. From the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Select the **Templates** tab.
3. In the row of the template you want to view, click the menu icon (<img src="../../../.gitbook/assets/menu icon (3).png" alt="" data-size="line">), and sele**ct View**.&#x20;

### Viewing a template uploaded to a specific Tenant

1. Select the Tenant that will use the template from the **Tenant** list box.
2. Navigate to **Automation** -> **Stacks**.
3. In the row of the template you want to view, click the menu icon (<img src="../../../.gitbook/assets/menu icon (3).png" alt="" data-size="line">), and select **View**.&#x20;

## Downloading a template

### Downloading a template available to all Tenants

1. From the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Select the **Templates** tab.
3. In the row of the template you want to Download, click the menu icon (<img src="../../../.gitbook/assets/menu icon (3).png" alt="" data-size="line">), and select **Download**.&#x20;

### Downloading a template uploaded to a specific Tenant

1. Select the Tenant that will use the template from the **Tenant** list box.
2. Navigate to **Automation** -> **Stacks**.
3. In the row of the template you want to Download, click the menu icon (<img src="../../../.gitbook/assets/menu icon (3).png" alt="" data-size="line">), and select **Download**.&#x20;

## Deleting a template

### Deleting a template available to all Tenants

1. From the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Select the **Templates** tab.
3. In the row of the template you want to delete, click the menu icon (<img src="../../../.gitbook/assets/menu icon (3).png" alt="" data-size="line">), and select **Delete**.&#x20;

### Deleting a template uploaded to a specific Tenant

1. Select the Tenant that will use the template from the **Tenant** list box.
2. Navigate to **Automation** -> **Stacks**.
3. In the row of the template you want to delete, click the menu icon (<img src="../../../.gitbook/assets/menu icon (3).png" alt="" data-size="line">), and select **Delete**.&#x20;

## Deploying a Stacks template

1. Select the Tenant from the **Tenant** list box.
2. Navigate to **Automation** -> **Stacks**.&#x20;
3. Select the **Deployments** tab.
4. Click **Deploy**. The **Deploy Template** pane displays.
5. Enter a deployment name in the **Name** field.
6. Select how you will provide a template:&#x20;
   * **Upload File**: Click **Choose File** and select the file to upload.
   * **Select Template**:  From the **Deploy Template** list box, select the template to deploy.&#x20;
7. Click **Next**.&#x20;
8. &#x20;If a dialog box displays, enter values for any necessary input variables, and click **Next**.
9. Click **Deploy**. Resources from the selected template are deployed into the selected Tenant.

## Viewing Stacks deployments

View a deployment's logs or configurations (in JSON).

1. Select the Tenant from the **Tenant** list box.
2. Navigate to **Automation** -> **Stacks**.&#x20;
3. Select the **Deployments** tab.
4. Click on the deployment you want to view in the **NAME** column. Details for the selected deployment display.
5. On the left is a list of **Resources** organized hierarchically. Select the resource(s) you want to investigate.
6. On the right, details for the selected resource(s) display. Select **JSON** or **Logs** to inspect specific configurations or logs for that resource.
7. Click **Close** to return to the **Deployments** tab.&#x20;
