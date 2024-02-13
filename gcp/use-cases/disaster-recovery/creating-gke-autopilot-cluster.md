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

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

This takes about 20 minutes.  Infrastructure status should move to Completed. At the end of it, double-check that a "plan" (Administrators --> Plans) has been created with the same name (nonprod).
