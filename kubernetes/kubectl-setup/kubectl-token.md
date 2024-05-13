---
description: Set up KubeCtl within the DuploCloud Portal by downloading the token and configuring Mirantis Lens for DuploCloud authentication.
---

# KubeCtl Token and Mirantis Lens Configuration

## Downloading the KubeCtl token

DuploCloud provides a way to connect directly to the Cluster namespace using the `kubectl` token. This facilitates direct interaction with your Kubernetes cluster through a command-line interface.

{% hint style="warning" %}
If you attempt to start a **KubeCtl Shell** instance and receive a **503** in your web browser, ensure that the **duplo-shell** service in the **Default** Tenant is running and that the Hosts which support it are running, as well.
{% endhint %}

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Services**.
2. From the **KubeCtl** list box, select **KubeCtl Token.** The **Token** window displays. **Copy** the contents to your clipboard.

<figure><img src="../../.gitbook/assets/Screenshot (349).png" alt=""><figcaption><p>The <strong>Kubernetes Services</strong> page with <strong>KubeCtl Token</strong> button</p></figcaption></figure>

<div align="left">
<img src="../../.gitbook/assets/image (1) (3).png" alt="Token window with kubectl commands for creating token">
</div>

## Configuring Mirantis Lens for DuploCloud Authentication

To enhance your Kubernetes management experience, you can integrate Mirantis Lens with DuploCloud by following these steps:

1. **Install DuploCloud Client:** Ensure the `duploctl` command-line tool is installed. If not, use `pip install duplocloud-client` to install it.
2. **Install Lens Client:** Download and install the Lens Kubernetes IDE client from its official website.
3. **Generate Kubeconfig File:** With `duploctl`, generate a kubeconfig file for Lens connection:
   ```
   duploctl jit update_kubeconfig --plan nonprod01 --tenant $DUPLO_TENANT --host https://$DUPLO_HOST --token $DUPLO_TOKEN
   ```
4. **Add Kubeconfig to Lens:** In Lens, navigate to "Catalog" and use the `+` button to add the kubeconfig file, configuring Lens to connect to your Kubernetes cluster.
5. **Connect to the Cluster:** Lens will prompt for login through a browser window. For private EKS clusters, ensure VPN connectivity for authentication.

**Note:** After your session, disconnect from the cluster to avoid repeated browser tab openings during re-authentication attempts.

Integrating Mirantis Lens with DuploCloud enhances your Kubernetes cluster management by providing a powerful graphical interface alongside the direct command-line access provided by the `kubectl` token.