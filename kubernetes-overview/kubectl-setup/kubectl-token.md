---
description: >-
  Set up KubeCtl within the DuploCloud Portal by downloading the token and
  configuring Mirantis Lens for DuploCloud authentication.
---

# KubeCtl Token

## KubeCtl Token and Mirantis Lens Configuration

### Downloading the KubeCtl token

DuploCloud lets you connect directly to the Cluster namespace using the `kubectl` token. This facilitates direct interaction with your Kubernetes cluster through a command-line interface.

{% hint style="warning" %}
If you attempt to start a KubeCtl Shell instance and receive a 503 in your web browser, ensure that the Duplo-shell Service in the Default Tenant and the Hosts that support it are running.
{% endhint %}

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Services**.
2. From the **KubeCtl** list box, select **KubeCtl Token**. The **Token** window displays. Copy the contents to your clipboard.

<figure><img src="../../.gitbook/assets/Screenshot (349).png" alt=""><figcaption><p>The <strong>Kubernetes Services</strong> page with <strong>KubeCtl Token</strong> button</p></figcaption></figure>

<div align="left">

<img src="../../.gitbook/assets/image (194).png" alt="Token window with kubectl commands for creating token">

</div>

### Configuring Mirantis Lens for DuploCloud Authentication

To enhance your Kubernetes management experience, you can integrate Mirantis Lens with DuploCloud by following these steps:

1. **Install DuploCloud Client:** Ensure the `duploctl` command-line tool is installed. If not, use the `pip install duplocloud-client` command to install it.
2. **Install Lens Client:** Download and install the Lens Kubernetes IDE client from its official website.
3.  **Generate Kubeconfig File:** Using`duploctl`, generate a `kubeconfig` file for Lens connection, as follows:\


    ```
    duploctl jit update_kubeconfig --plan nonprod01 --tenant $DUPLO_TENANT --host https://$DUPLO_HOST --token $DUPLO_TOKEN
    ```
4. **Add Kubeconfig to Lens:** In Lens, navigate to **Catalog** and use the `+` button to add the `kubeconfig` file and configure Lens to connect to your Kubernetes cluster.
5. **Connect to the Cluster:** Lens will prompt for a login through a browser window. For private EKS cluster authentication, ensure VPN connectivity.

**Note:** Disconnect from the cluster after your session to avoid repeated browser tab openings during re-authentication attempts.

Integrating Mirantis Lens with DuploCloud enhances your Kubernetes cluster management by providing a powerful graphical interface alongside the direct command-line access provided by the `kubectl` token.
