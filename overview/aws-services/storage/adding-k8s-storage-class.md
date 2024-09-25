---
description: Set up Storage Classes and PVCs in Kubernetes
---

# Storage Class and PVCs

### **Step 1:** Create an Amazon EFS &#x20;

&#x20;Refer to steps [here](../../../aws-user-guide/aws-services/elastic-file-system-efs/)

### Step 2:  Create Storage Class with EFS Parameter

Navigate to  **Kubernetes** -> **Storage** -> **Storage Class**

Configure EFS parameter created at Step1 by clicking on EFS Parameter.

![K8s Storage Class Page](<../../../.gitbook/assets/image (166).png>)

### Step3: Create Persistent Volume (PVC) using Storage Class

Here, we are configuring Kubernetes to use Storage Class created in Step2 above, to create a Persistent Volume with 10Gi of storage capacity and ReadWriteMany access mode.

![K8s Storage Class (Persistent Volume Claim Tab)](<../../../.gitbook/assets/image (61).png>)



### Step4:  Mount PVC to the POD Deployment

Configure below in **Volumes** to create your application deployment using this PVC.&#x20;

{% code title="Volumes field" %}
```
# Deployment using PersistentVolumeClaim. 
- Name: <volumne name>
  Path: <mount path>
  Spec:
    PersistentVolumeClaim:
      claimName: <pvc name>
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.19-16_11_54.png" alt=""><figcaption><p>Services Page</p></figcaption></figure>
