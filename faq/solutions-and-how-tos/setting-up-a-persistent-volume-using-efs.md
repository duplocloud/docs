---
description: How to set up a persistent volume using EFS
---

# Setting Up a Persistent Volume Using EFS

Configure an Amazon EFS volume in DuploCloud and connect it to Kubernetes workloads through a Persistent Volume Claim (PVC), allowing your workloads to share storage across pods and persist data across container restarts and redeployments.

### Step 1: Create an EFS in DuploCloud

1. In the DuploCloud Portal, navigate to **Cloud Services** → **Storage** → **EFS**.
2.  Click **Add**. The **Add Elastic File System** pane displays.<br>

    <figure><img src="../../.gitbook/assets/image (500).png" alt=""><figcaption><p><strong>Add Elastic File System</strong> pane</p></figcaption></figure>
3. Complete the fields as follows:

<table data-header-hidden><thead><tr><th width="217.33331298828125">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the EFS.</td></tr><tr><td><strong>Performance Mode</strong></td><td>Select <strong>General Purpose</strong>.</td></tr><tr><td><strong>Throughput Mode</strong></td><td>Select <strong>Bursting</strong>.</td></tr><tr><td><strong>Enable Backup</strong></td><td>Select <strong>Disabled</strong>.</td></tr><tr><td><strong>Enable Encryption</strong></td><td>Select <strong>Enable</strong>.</td></tr></tbody></table>

4. Click **Submit**.

### Step 2: Create a Storage Class

1. In the DuploCloud Portal, go to **Kubernetes** → **Storage** → **Storage Class**.
2.  Click **Add**. The **Add Kubernetes Storage Class** pane displays.<br>

    <figure><img src="../../.gitbook/assets/Screenshot (980).png" alt=""><figcaption><p><strong>Add Kubernetes Storage Class</strong> pane</p></figcaption></figure>
3. Complete the fields as follows:

<table data-header-hidden><thead><tr><th width="204">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the storage class.</td></tr><tr><td><strong>Provisioner</strong></td><td>Select <strong>efs.csi.aws.com</strong>.</td></tr><tr><td><strong>Reclaim Policy</strong></td><td>Select <strong>Delete</strong>.</td></tr><tr><td><strong>Volume Binding Mode</strong></td><td>Select <strong>Immediate</strong>.</td></tr><tr><td><strong>Parameters</strong></td><td>Click <strong>Set EFS parameters</strong>, and in the <strong>File System Id</strong> field, select the EFS created in Step 1.</td></tr></tbody></table>

4. Click **Add**.

### Step 3: Create a Persistent Volume Claim (PVC)

1. In the DuploCloud Portal, navigate to **Kubernetes** → **Storage** → **Persistent Volume Claims**.
2.  Click **Add**. The **Add Kubernetes Persistent Volume Claim** pane displays.<br>

    <figure><img src="../../.gitbook/assets/Screenshot (981).png" alt=""><figcaption><p><strong>Add Kubernetes Persistent Volume Claim</strong> pane</p></figcaption></figure>
3. Complete the fields as follows:

<table data-header-hidden><thead><tr><th width="216.44439697265625">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the PVC.</td></tr><tr><td><strong>Storage Class Name</strong></td><td>Select the storage class created in Step 2.</td></tr><tr><td><strong>Volume Name</strong></td><td>Enter the same name you entered for the PVC in the <strong>Name</strong> field.</td></tr><tr><td><strong>Volume Mode</strong></td><td>Select <strong>Filesystem</strong>.</td></tr><tr><td><strong>Access Modes</strong></td><td>Select <strong>ReadWriteMany</strong>.</td></tr><tr><td><strong>Resources</strong></td><td>Enter the storage size you need (default is <strong>10Gi</strong>).</td></tr></tbody></table>

4. Click **Add**.

### Step 4: Update Service Configuration

Update your Service configuration to include the new PVC.&#x20;

1. Navigate to **Kubernetes** -> **Services.**
2. For the Service that needs the volume, click on the menu icon (<img src="../../.gitbook/assets/menu icon (32).avif" alt="" data-size="line">) and select **Edit**.
3. Click **Next**.&#x20;
4.  Update the **Volumes** field as shown in the example YAML snippet below.<br>

    <figure><img src="../../.gitbook/assets/Screenshot (962) (1).png" alt=""><figcaption><p><strong>Edit Service</strong> pane with PVC configurations in the <strong>Volumes</strong> field</p></figcaption></figure>

```yaml
volumes:
  - name: <volume-name>                  # Replace with a name for this volume
    path: <mount-path>                   # Replace with the path inside the container
    spec:
      persistentVolumeClaim:
        claimName: <pvc-name>           # Replace with the name of your PersistentVolumeClaim
```

5. Click **Update** to apply the changes to the Service.
6. Restart the Service and ensure the Pod restarts and mounts the volume successfully.

{% hint style="info" %}
**Note:** Restarting the Service is required for changes to take effect. Plan for a brief downtime during this configuration.
{% endhint %}
