---
description: Deploy Kubernetes Helm Charts with DuploCloud
---

# Helm Charts

[Helm Charts](https://helm.sh/docs/topics/charts/) are packages of pre-configured Kubernetes resources that help you define, install, and upgrade Kubernetes applications. You can integrate Helm Charts with DuploCloud to deploy applications onto the Kubernetes clusters you've created in DuploCloud. For Helm Charts general guidance and best practices, see the [Helm Charts Info](../../extras-overview/helm-charts.md) page in the DuploCloud Extras section.

{% hint style="info" %}
Helm Charts are only supported for administrator-level DuploCloud users.
{% endhint %}

## **Prerequisites**&#x20;

* Ensure you have a Kubernetes cluster set up in DuploCloud.&#x20;
* [Install Helm](https://github.com/helm/helm/releases) on your local machine or a machine with access to your Kubernetes cluster.

## **Creating Helm Charts**

Identify the Helm charts you want to use for deploying your applications or services.

You can use community-maintained charts from public repositories like [Artifact Hub](https://artifacthub.io/), or you can create your own custom charts tailored to your specific needs.

To create custom Helm charts, modify the values.yaml or create custom templates as necessary. This might involve configuring resource limits, environment variables, or other settings specific to your deployment.&#x20;

You can also modify Helm Chart values using the node selector. This is the most common method. For example, to deploy a chart into the duploservices-mytenant Tenant using the node selector, give:

{% code fullWidth="false" %}
```yaml
nodeSelector:
  tenantname: duploservices-mytenant
```
{% endcode %}

To specify which hosts the chart should run on using the node selector with  allocation tags, give:

```yaml
nodeSelector:
  tenantname: duploservices-mytenant
  allocationtags: mychart
```

## **Adding Helm Repositories in DuploCloud**

1. From the DuploCloud Portal, navigate to **Kubernetes** -> **Helm**.
2. Select the **Repository** tab, and click **Add**. The **Add Helm Repository** pane displays.

<div align="left"><figure><img src="../../.gitbook/assets/Add helm repository.png" alt=""><figcaption><p>The <strong>Add Helm Repository</strong> pane in the DuploCloud Portal</p></figcaption></figure></div>

3. In the **Name** field, enter the repository name.
4. In the **Interval** field, select the interval (the frequency with which the tool should check for changes in the repository and reconcile those changes in the Kubernetes cluster).
5. In the **Repository URL** field, enter the repository URL.&#x20;
6. Click **Create**. The Helm repository is added.

## Managing Helm Repositories

Once you've added a Helm repository, you can view its details, update its configuration, or delete from directly in the DuploCloud Portal.

1. Navigate to **Kubernetes** → **Helm.**
2. Select the **Repository** tab.
3. Click the menu icon (<img src="../../.gitbook/assets/menu icon (14).avif" alt="" data-size="line">) in the row of the repository you want to manage.
4. Choose one of the following actions:

<table data-header-hidden><thead><tr><th width="146.4444580078125">Option</th><th>Description</th></tr></thead><tbody><tr><td><strong>View</strong></td><td>View the repository’s current configuration, sync status, and metadata.</td></tr><tr><td><strong>Update</strong></td><td>Edit the repository name, URL, sync interval, or authentication settings.</td></tr><tr><td><strong>Delete</strong></td><td>Remove the repository from DuploCloud. Releases that depend on it will no longer reconcile.</td></tr></tbody></table>

{% hint style="info" %}
Deleting a Helm repository will not remove any releases that were deployed from it, but those releases will no longer reconcile unless the repository is re-added.
{% endhint %}

## **Deploying a Helm Release**

Deploy a Kubernetes cluster using a Helm Chart from the DuploCloud Platform.&#x20;

1. From the DuploCloud Portal, navigate to **Kubernetes** → **Helm**.
2. Select the **Release** tab, and click **Add**. The **Add Helm Release** page displays

<figure><img src="../../.gitbook/assets/Screenshot (476) (1).png" alt=""><figcaption><p>The <strong>Add Helm Release</strong> page in the DuploCloud Portal</p></figcaption></figure>

3. In the **Name** field, enter a unique name for this Helm release (e.g., `nginx-release`).
4. In the Release **Name** field, enter the name to identify the application deployment in Kubernetes (e.g., `nginx-release`).
5. In the **Interval (MM: SS)** box, set the time interval for periodic reconciliation of the release (e.g., `02:00`).
6. In the **Chart Name** field, specify the name of the Helm chart to use (e.g., `nginx`).
7. In the **Version** field, specify the specific version of the Helm chart to deploy (e.g., `15.1.0`).
8. From the **Reconcile Strategy** list box, select how Helm ensures the deployment stays consistent (e.g., `Chart Version`).
9. From the **Source Type** list box, choose where the Helm chart is stored (e.g., `HelmRepository`).
10. From the **Source Name** list box, select the name of the Helm repository or source.
11. In the **Interval (MM: SS)** box, select the frequency with which the tool should check for changes in the repository and reconcile those changes in the Kubernetes cluster.
12. In the **Values** field, add any custom configuration values in YAML format to override the defaults (e.g., replica count or enabling a service account).
13. Click **Add**. The Helm release is deployed. To check the release status, navigate to **Kubernetes** -> **Helm**, and select the **Release** tab.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot (477) (1).png" alt=""><figcaption><p>The <strong>Release</strong> tab on the Kubernetes <strong>Helm</strong> page</p></figcaption></figure>

## **Viewing Helm Deployments**

Navigate to the **Services** page (**Kubernetes** → **Services**) to view a list of all deployed services, including those created using Helm Charts. Use this view to confirm that the service has deployed without errors and all components are running as expected.

* Helm-deployed services are displayed in **read-only mode**. This means:
  * You can **view details** (e.g., replicas, resource allocation, logs) to confirm that the service is functioning as expected.
  * However, you **cannot modify the service** directly in DuploCloud. Any changes to the service must be made by updating the Helm chart and redeploying it.

<figure><img src="../../.gitbook/assets/helm release services.png" alt=""><figcaption><p>The Kubernetes <strong>Services</strong> page with the read-only nginx-release Service highlighted</p></figcaption></figure>

Click on the name of the Service in the **NAME** column to view details.

<figure><img src="../../.gitbook/assets/HELM SERVICE DETAILS.png" alt=""><figcaption><p>The details page for the Service created using Helm Charts</p></figcaption></figure>
