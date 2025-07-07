# OCI Helm Repositories

DuploCloud supports OCI-compliant Helm repositories, enabling you to manage and deploy Helm charts stored in container registries such as Docker Hub, GitHub Container Registry, Amazon ECR, and Azure Container Registry. This support is especially useful for managing private Helm charts or leveraging cloud-native registries that follow the OCI distribution specification.

## Prerequisites

* A Kubernetes cluster set up in DuploCloud.
* Access credentials (if required) for your OCI-compliant registry.
* Helm CLI installed on your local machine (optional but recommended for testing).

## Adding an OCI Helm Repository

To register an OCI Helm repository in DuploCloud:

1. In the DuploCloud Portal, navigate to **Kubernetes** → **Helm.**
2. Select the **Repository** tab.
3. Click **Add**, The **Add Helm Repository** pane displays.
4. Complete the fields as described below:

<table data-header-hidden><thead><tr><th width="245.99993896484375"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a friendly name for the repository.</td></tr><tr><td><strong>Interval (MM:SS)</strong></td><td>Set how often DuploCloud should refresh and synchronize with the repository. The default is 05:00 (five minutes).</td></tr><tr><td><strong>Repository Type</strong></td><td>Select <strong>OCI Repository</strong></td></tr><tr><td><strong>Repository URL</strong></td><td>Enter the full OCI repository URL, for example, <code>oci://ghcr.io/my-org/charts</code>.</td></tr></tbody></table>

4. Click **Create**. Once added, the OCI repository will appear under the **Repository** tab and be available when [deploying Helm charts](helm-charts.md#deploying-helm-releases).

## Managing an OCI Repository

Once you've added an OCI Helm repository, you can view its details, update its configuration, or delete from directly in the DuploCloud Portal.

1. Navigate to **Kubernetes** → **Helm.**
2. Select the **Repository** tab.
3. Click the **menu icon (three dots)** in the row of the repository you want to manage.
4. Choose one of the following actions:

<table data-header-hidden><thead><tr><th width="146.4444580078125">Option</th><th>Description</th></tr></thead><tbody><tr><td><strong>View</strong></td><td>View the repository’s current configuration, sync status, and metadata.</td></tr><tr><td><strong>Update</strong></td><td>Edit the repository name, URL, sync interval, or authentication settings.</td></tr><tr><td><strong>Delete</strong></td><td>Remove the repository from DuploCloud. Releases that depend on it will no longer reconcile.</td></tr></tbody></table>

{% hint style="info" %}
Deleting a Helm repository will not remove any releases that were deployed from it, but those releases will no longer reconcile unless the repository is re-added.
{% endhint %}

## Deploying Charts from an OCI Repository

Once your OCI repository is added and synced in DuploCloud, you can deploy charts from it the same way you would for any other Helm repository. Follow the steps in [Deploying a Helm Release](helm-charts.md#deploying-helm-releases), selecting your OCI repository from the **Source Name** list box.

