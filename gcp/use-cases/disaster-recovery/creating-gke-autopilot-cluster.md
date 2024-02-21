# Creating GKE Autopilot Cluster

Navigate from **Administrator** -> **Infrastructure** -> **Add** to create Infrastructure with GKE Standard Cluster.

* Name: nonprod
* Account: Google Cloud account
* VPC CIDR: 10.11.0.0/16
* Cloud: Google
* Region: us-east1
* Subnet CIDR: 22
* Enable GKE: enabled
* Cluster Mode: GKE Autopilot

<div align="left">

<figure><img src="../../../.gitbook/assets/image (2) (1) (6).png" alt=""><figcaption><p><strong>Add infrastructure</strong> page</p></figcaption></figure>

</div>

This takes about 20 minutes.  Infrastructure status should move to Completed. Once the Infrastructure status shows Complete, navigate to **Administrators** -> **Plans** to verify that a plan has been created with the same name (nonprod).
