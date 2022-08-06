# Adding K8s Storage Class

### **Step1:** Create an Amazon EFS &#x20;

&#x20;Refer to steps [here](../elastic-file-system-efs.md)

### Step2:  Create Storage Class with EFS Parameter

Navigate to  **DevOps** > **Containers** > **EKS/Native > Storage Class**

Configure EFS parameter created at Step1 by clicking on EFS Parameter.

![K8s Storage Class Page](<../../../.gitbook/assets/image (49).png>)

### Step3: Create Persistent Volume (PVC) using Storage Class

Here, we are configuring Kubernetes to use Storage Class created in Step2 above, to create a Persistent Volume with 10Gi of storage capacity and ReadWriteMany access mode.

![K8s Storage Class (Persistent Volume Claim Tab)](<../../../.gitbook/assets/image (40).png>)



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

![Services Page](<../../../.gitbook/assets/image (34) (1).png>)
