# Argo Workflows

[Argo Workflows](https://argo-workflows.readthedocs.io/en/stable/) is a Kubernetes-native workflow engine used to create, run, and manage CI/CD pipelines, data processing workflows, and other automated tasks.

In DuploCloud, Argo Workflows runs within your EKS cluster and leverages the platform’s permissions, namespace isolation, and monitoring features.

From the Argo Workflows page, you can:

* Create and manage Workflow Templates (reusable workflow definitions).
* Launch and monitor Workflows (actual workflow executions based on Workflow Templates).

## Prerequisites&#x20;

### **Configure Argo Workflows Infrastructure Settings**

Before using Argo Workflows in a Tenant, make sure the following infrastructure settings are configured:

1. Navigate to **Administrator** → **Infrastructure**.
2. Select the Infrastructure from the **NAME** column.
3. Go to the **Settings** tab and click **Add**. The **Infra – Set Custom Data** pane displays.
4. In the **Setting Name** field, select **Duplo CI – Argo Workflows Tenant**.
5. Choose one or more Tenants where Argo Workflows will run.
6. Click **Set** to save the configuration.
7. Repeat steps 3–6 to add another setting.
   * This time, in step 4, select **Duplo CI – Argo Workflows Certificate** and choose an ACM certificate to enable HTTPS access to the Argo Workflows UI.
8. Click **Set** to save the certificate configuration.

<figure><img src="../../.gitbook/assets/argo settings.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note:** Every Tenant that will use Argo Workflows must have the **Tenant** setting configured.&#x20;
{% endhint %}

## Adding a Workflow Template

Workflow Templates define reusable workflows that can be executed multiple times. Complete the following steps to add a Workflow Template.

1. From the DuploCloud Portal, navigate to **CI/CD** -> **Argo Workflows**.&#x20;
2. Select the **Workflow Templates** tab.
3.  Click **Add**. The **Add Workflow Template** pane displays. <br>

    <figure><img src="../../.gitbook/assets/Screenshot (1048).png" alt=""><figcaption><p><strong>Add Workflow Template</strong> pane</p></figcaption></figure>
4. Click **Choose File** and select a YAML file containing your workflow definition (the file must follow Argo Workflow YAML specifications) or paste the YAML directly into the **Workflow Template Data** field.
5. Click **Create**. The template appears in the Workflow Templates list.

{% hint style="info" %}
**Notes:**

* Templates can be edited or deleted later.
* Multiple workflows can be created from the same template.
{% endhint %}

## Managing Workflow Templates

View, edit, or delete Workflow Templates from directly in the DuploCloud Portal.

### Viewing and Editing a Workflow Template

1. From the DuploCloud Portal, navigate to **CI/CD** -> **Argo Workflows**.&#x20;
2. Select the **Workflow Templates** tab.
3. Click the Workflow Template name in the **NAME** column to display the details page. The **Description** field shows the YAML definition of the template, including the template name, entry point, workflow steps, container image, commands, arguments, and any input parameters.
4. To modify workflow parameters, click **Actions** and select **Edit**.&#x20;
5. Edit the Workflow as needed and click **Update** to save your changes.

### Deleting a Workflow Template

1. From the DuploCloud Portal, navigate to **CI/CD** -> **Argo Workflows**.&#x20;
2. Select the **Workflow Templates** tab.
3. Click the menu icon (three dots) in the row of the Workflow Template you want to delete, and select **Delete**.

## Launching a Workflow

Start a new workflow run from a Workflow Template.

1. From the DuploCloud Portal, navigate to **CI/CD** -> **Argo Workflows**.&#x20;
2. Select the **Workflow Templates** tab.
3. Click the **m**enu icon (<img src="../../.gitbook/assets/menu icon (27).avif" alt="" data-size="line">) next to the template you want to run and select **Launch Workflow**.
4.  The **Launch Workflow** pane displays. Click **Create** to launch the workflow.<br>

    <figure><img src="../../.gitbook/assets/Screenshot (1047).png" alt=""><figcaption><p><strong>Launch Workflow</strong> pane</p></figcaption></figure>
5. A new workflow run is created from the template and will appear in the **Workflows** tab.

## Viewing Workflows

View workflow executions in your Tenant from the **Workflows** tab.

1. Navigate to **CI/CD** → **Argo Workflows** in the DuploCloud Portal.
2. Select the **Workflows** tab.
3. Click on the Workflow you want to view details for in the **NAME** column (use the **Search** box to find a specific workflow, if needed). The Workflow details page displays.
4. Select the **Steps**, **Logs**, or **Definition** tab to view Workflow information:
   * **Steps**: Shows a visual breakdown of the workflow’s execution hierarchy. Each step and sub-step appears in the order they were run, giving you a clear picture of the workflow’s structure. Clicking any step opens its corresponding logs.

<figure><img src="../../.gitbook/assets/Screenshot (1077) (1).png" alt=""><figcaption><p>The <strong>Steps</strong> tab for an Argo Workflow in the DuploCloud Portal</p></figcaption></figure>

* **Logs**: Displays the output for each step of the workflow. Selecting a step in the sidebar loads its logs.

<figure><img src="../../.gitbook/assets/Screenshot (1078) (1).png" alt=""><figcaption><p><strong>Logs</strong> tab for an Argo Workflow in the DuploCloud Portal</p></figcaption></figure>

* **Definition**: Displays the full YAML for the workflow run. This includes the executed entry point, steps, container images, commands, arguments, input parameters, and any runtime values.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot (1079) (1).png" alt=""><figcaption><p><strong>Definition</strong> tab for an Argo Workflow in the DuploCloud Portal</p></figcaption></figure>
