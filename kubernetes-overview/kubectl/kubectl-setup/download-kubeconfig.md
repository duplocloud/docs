---
description: Download kubeconfig to interact with Kubernetes clusters using kubectl
---

# Download Kubeconfig

The `kubeconfig` file is a configuration file used by `kubectl` to connect to a Kubernetes cluster. It contains essential information such as the cluster's API server address, authentication credentials, and context settings that define which cluster and namespace `kubectl` should interact with. The `kubeconfig` file tells `kubectl` how to connect to the desired Kubernetes cluster and which permissions to use. By default, `kubeconfig` is saved in the `$HOME/` directory in the Linux operating system. Refer to [this article](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/) for more information about `kubeconfig`.

## Downloading `kubeconfig`

1. In the DuploCloud Portal, navigate to **Administrators** -> **Infrastructure.**
2. In the **NAME** column, select the Infrastructure where you want to set up `kubectl`.&#x20;
3. Click the **EKS** (for AWS), **GKE** (for GCP), or the **AKS** (for Azure) tab. The **Download Kubeconfig For Plan** pane displays.
4. Click **Download Kubeconfig** to download the `kubeconfig` file.

<figure><img src="../../../.gitbook/assets/Screenshot (346).png" alt=""><figcaption><p>The <strong>EKS</strong> tab for the TEST01 Infrastructure. </p></figcaption></figure>

{% hint style="info" %}
If you don't have Administrator access, you can use `duplo-jit` to access Kubernetes. When you click **Download kubeconfig**, the **Access to Kubernetes from your Workstation** window gives you the option to install [`duplo-jit`](../../../aws-user-guide/use-cases/jit-access.md) to access your Kubernetes cluster without obtaining permanent access keys.
{% endhint %}

<div align="left">

<figure><img src="../../../.gitbook/assets/kubeconfig_dialog.png" alt=""><figcaption><p><strong>Access to Kubernetes from your Workstation</strong> pane</p></figcaption></figure>

</div>
