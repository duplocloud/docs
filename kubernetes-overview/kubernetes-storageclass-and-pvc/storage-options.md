---
description: Use Azure's built-in Kubernetes StorageClass constructs
---

# Native Azure Storage Classes

## Mounting Native Azure Built-In Storage Classes

AKS provides a few out-of-the-box StorageClass objects. To mount the built-in storage classes, configure `Volumes`  as below.

<div align="left">

<img src="../../.gitbook/assets/image (2) (4).png" alt="Service Deployment Page">

</div>

<pre data-title="Volumes field"><code><strong>- AccessMode: ReadWriteMany
</strong>  Name: data
  Path: /attachedvolume
  StorageClassName: azurefile #if empty default storage class will be used which is disk
  Size: 20Gi
</code></pre>
