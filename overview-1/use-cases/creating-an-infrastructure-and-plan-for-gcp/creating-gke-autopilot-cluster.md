# Creating a GKE Autopilot Cluster

When [creating an Infrastructure](./), use the **Enable GKE** toggle switch to enable GKE. In the Cluster Mode list box, select **GKE Autopilot**. Complete the remaining fields (**GKE Version**, **GKE Endpoint Visibility**, and **Cluster IP CIDR**). Click **Create**.

<figure><img src="../../../.gitbook/assets/Screenshot (215) (1).png" alt=""><figcaption><p><strong>Add infrastructure</strong> page for GKE Autopilot</p></figcaption></figure>



This takes about 20 minutes.  Infrastructure status should move to Completed. Once the Infrastructure status shows Complete, navigate to **Administrators** -> **Plans** to verify that a Plan has been created with the same name (nonprod).
