# Storage options

DuploCloud Portal supports different configurations to achieve storage options in Azure.

## 1. Using StorageClass and PVC

### Create Storage Class

Navigate to **DevOps** > **Containers** > **AKS/Native** > **K8S Storage** Tab. Create a Storage Class from the screen below.

![sample StorageClass](<../../../.gitbook/assets/image (27).png>)

### Create PersistentVolumeClaims(PVC)

Follow [these steps to create PVC ](storage-options.md#create-persistentvolumeclaims-pvc)referring to the StorageClass created in the step above.

### Mount PersistentVolumeClaims(PVC) as Volume in Deployment

Follow [these steps to mount **** PVC Volume ](storage-options.md#mount-persistentvolumeclaims-pvc-as-volume-in-deployment)in the Service Deployment.

## 2. Using Built-In Storage Classes in AKS

AKS provides a few out-of-the-box StorageClass objects. To mount the built-in storage classes, configure `Volumes`  as below.

![Service Deployment Page](<../../../.gitbook/assets/image (2).png>)

<pre data-title="Volumes field"><code><strong>- AccessMode: ReadWriteMany
</strong>  Name: data
  Path: /attachedvolume
  StorageClassName: azurefile #if empty default storage class will be used which is disk
  Size: 20Gi</code></pre>

## **3. Using Kubernetes Secret with the Azure Storage connection data**

#### **Create Storage Account and File Shares**

Refer to steps to [configure the new Storage Account and FileShare](../storage-account.md) in Azure.

Copy Storage Account Key and FileShare Name from DuploCloud Portal for creating Kubernetes Secrets in the next step.

#### **Create Kubernetes Secret**

Navigate to **DevOps** > **Containers** > **AKS/Native** > **K8S Secrets**  Tab. Create Kubernetes Secret Object using Storage Account.

![Kubernetes Storage Account Secret](<../../../.gitbook/assets/image (34).png>)

{% code title="SecretDetails Example" %}
```
azurestorageaccountkey: >-
    <storage-account-key>
azurestorageaccountname: <storage-account-name>

```
{% endcode %}

#### Mount Azure Storage Connection in deployment

While creating a deployment, under **Other Pod Config** and **Other Container Config**, provide the configuration below to create and mount the storage volume for your service. In the configuration below, `shareName`attribute should be the [File Share name ](../storage-account.md#create-and-view-file-shares)which you can get from the Storage Account screen.

{% code title="Other Pod Config" overflow="wrap" %}
```
PodLabels:
  app: azuretest
Volumes:
  - name: azurefileshare
    azureFile:
      secretName: my-storage-account-key
      shareName: fileshare1
      readOnly: false
```
{% endcode %}

{% code title="Other Container Config" %}
```
VolumesMounts:
  - name: azurefileshare
    mountPath: /myfileshare
```
{% endcode %}

![Service Deployment Screen with K8s Secret example](<../../../.gitbook/assets/image (25).png>)
