---
description: Creating K8s PVCs and StorageClass constructs in the DuploCloud Portal
---

# Kubernetes StorageClass and PVC

## Configure Kubernetes Storage

You can configure the Storage Class and Persistent Volume Claims (PVCs) from the DuploCloud Portal.&#x20;

1. In the DuploCloud Portal, navigate to **DevOps** -> **Containers** -> _**CONTAINER\_TYPE**_, where _**CONTAINER\_TYPE**_ is **EKS/Native**, **AKS/Native** or **GKE/Native**.
2.  Click the **K8S Storage** tab. The **Kubernetes Storage** page displays. From this page, you define your Kubernetes [**Persistent Volume Claims**](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) and [**Storage Classes**](https://kubernetes.io/docs/concepts/storage/storage-classes/). The **Persistent Volume Claims** option is selected by default.

    <figure><img src="../../.gitbook/assets/GCP_K8S_Storage_PVC.png" alt=""><figcaption><p>The <strong>Persistent Volume Claims</strong> option on the <strong>Kubernetes Storage</strong> page</p></figcaption></figure>
3.  Click **Add**. The **Add Kubernetes Persistent Volume Claim** page displays.

    <figure><img src="../../.gitbook/assets/GCP_K8S_Storage_PVC_Form.png" alt=""><figcaption><p>The <strong>Add Kubernetes Persistent Volume Claim</strong> page</p></figcaption></figure>
4. Define the PVC **Name**, **Storage Class Name**, **Volume Name**, **Volume Mode**, and other details such as volume **Access Modes**.
5. Click **Add**.
6.  On the **Kubernetes Storage** page, select the **Storage Class** option.&#x20;

    <figure><img src="../../.gitbook/assets/GCP_K8S_Storage_Storage_Class.png" alt=""><figcaption><p>The <strong>Storage Class</strong> option on the <strong>Kubernetes Storage</strong> page</p></figcaption></figure>
7.  Click **Add**. The **Add Kubernetes Storage Class** page displays.

    <figure><img src="../../.gitbook/assets/GCP_K8S_Storage_Add_Storage_Class.png" alt=""><figcaption><p>The <strong>Add Kubernetes Storage Class</strong> page</p></figcaption></figure>
8. Define the Storage Class **Name**, **Provisioner**, **Reclaim Policy**, and **Volume Binding Mode.** Select other options, such as whether to **Allow Volume Expansion**.
9. Click **Add**.

## Creating a Storage Class

1. In the DuploCloud Portal, navigate to **DevOps** > **Containers** >  _**CONTAINER\_TYPE**_, where _**CONTAINER\_TYPE**_ is **EKS/Native**, **AKS/Native** or **GKE/Native**.&#x20;
2. Click the **K8S Storage** tab.
3. Click **Add**. The **Add Kubernetes Storage Class** page displays.
4. Create a Storage Class, as in the example below.

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p><strong>Add Kubernetes Storage Class</strong> page </p></figcaption></figure>

{% hint style="info" %}
For information on using Native Azure StorageClasses, [see this section](storage-options.md).
{% endhint %}
