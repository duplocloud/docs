---
description: Manage and deploy Helm charts stored in OCI-compliant registries
---

# OCI Helm Repositories

OCI Helm repositories let you store and manage Helm charts as OCI artifacts, similar to container images. This approach is useful for cloud-native registries and private charts where a traditional `index.yaml` catalog is not available.

Using OCI repositories in DuploCloud, you can deploy charts just like a standard Helm repository, while taking advantage of OCI-native workflows.

## Prerequisites

* A Kubernetes cluster set up in DuploCloud.
* Access credentials (if required) for your OCI-compliant registry.
* Helm CLI installed on your local machine (optional but recommended for testing).

## Adding an OCI Helm Repository

To register an OCI Helm repository in DuploCloud:

1. In the DuploCloud Portal, navigate to **Kubernetes** → **Helm.**
2. Select the **OCI Repository** tab.
3.  Click **Add**, The **Add OCI Repository** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (933).png" alt="" width="411"><figcaption><p><strong>Add OCI Repository</strong> pane</p></figcaption></figure></div>
4. Complete the fields as described below:

<table data-header-hidden><thead><tr><th width="199.5555419921875">Field</th><th>Description / Notes</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter the repository name. This field is required.</td></tr><tr><td><strong>Interval (MM:SS)</strong></td><td>Enter the synchronization interval in minutes and seconds. The default is <strong>05:00</strong>.</td></tr><tr><td><strong>Repository URL</strong></td><td>Enter the OCI repository URL. For example: <code>oci://registry-1.docker.io/bitnamicharts/nginx</code></td></tr><tr><td><strong>Tag</strong></td><td>Enter a tag for the repository, for example, <code>18.9.0</code>.</td></tr><tr><td><strong>Media Type</strong></td><td>Select the media type from the available options.</td></tr><tr><td><strong>Operation</strong></td><td>Select the operation to perform from the available options.</td></tr></tbody></table>

5. Click **Create**. Once added, the repository will appear under the **OCI Repository** tab and be available when [deploying Helm charts](helm-charts.md#deploying-helm-releases).

## Managing an OCI Repository

Once you've added an OCI Helm repository, you can view its details, update its configuration, or delete from directly in the DuploCloud Portal.

1. Navigate to **Kubernetes** → **Helm.**
2. Select the **OCI Repository** tab.
3. Click the **menu icon** (<img src="../../../.gitbook/assets/menu icon (26).avif" alt="" data-size="line">) in the row of the repository you want to manage.
4. Choose one of the following actions:

<table data-header-hidden><thead><tr><th width="146.4444580078125">Option</th><th>Description</th></tr></thead><tbody><tr><td><strong>View</strong></td><td>View the repository’s current configuration, sync status, and metadata.</td></tr><tr><td><strong>Update</strong></td><td>Edit the repository name, URL, sync interval, or authentication settings.</td></tr><tr><td><strong>Delete</strong></td><td>Remove the repository from DuploCloud. Releases that depend on it will no longer reconcile.</td></tr></tbody></table>

{% hint style="info" %}
Deleting an OCI Helm repository will not remove any releases that were deployed from it, but those releases will no longer reconcile unless the repository is re-added.
{% endhint %}

<figure><img src="../../../.gitbook/assets/Screenshot (935).png" alt=""><figcaption><p><strong>OCI Helm Repository-View</strong> pane</p></figcaption></figure>

## Deploying a Helm Release from an OCI Repository

To deploy a Helm release from an OCI-compliant repository, see the documentation for [Deploying Helm Releases](helm-charts.md#deploying-a-helm-release).

When completing the release fields:

* For **Source Type**, select **OCIRepository**.
* For **Source Name**, select the OCI repository you added.

The release will deploy using the selected OCI repository and appear under the **Release** tab.
