---
description: Using K8s Secrets with Azure Storage Accounts
---

# Using Kubernetes Secrets with Azure Storage connection data

### **Create Storage Account and File Shares**

Refer to steps to [configure the new Storage Account and FileShare](../../azure/azure-services/storage-account.md) in Azure.

Copy Storage Account Key and FileShare Name from DuploCloud Portal for creating Kubernetes Secrets in the next step.

### **Create Kubernetes Secret**

Navigate to **Kubernetes** -> **Secrets**. Create a Kubernetes Secret Object using an Azure Storage Account.&#x20;

For more information, see [Kubernetes Configs and Secrets](./).

<figure><img src="../../.gitbook/assets/image (112).png" alt=""><figcaption><p>Kubernetes Storage Account Secret</p></figcaption></figure>

{% code title="SecretDetails example" %}
```
azurestorageaccountkey: >-
    <storage-account-key>
azurestorageaccountname: <storage-account-name>
```
{% endcode %}

### Mount the Azure Storage Connection in your deployment

While creating a deployment, under **Other Pod Config** and **Other Container Config**, provide the configuration below to create and mount the storage volume for your service. In the configuration below, `shareName`attribute should be the [File Share name ](../../azure/azure-services/storage-account.md#create-and-view-file-shares)which you can get from the Storage Account screen.

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

<figure><img src="../../.gitbook/assets/image (113).png" alt=""><figcaption><p>Service Deployment Screen with K8s Secret example</p></figcaption></figure>
