# Creating GKE Standard Cluster

Navigate from **Administrator** -> **Infrastructure** -> **Add** to create Infrastructure with GKE Standard Cluster.

* Name: nonprod
* Account: Google Cloud account
* VPC CIDR: 10.11.0.0/16
* Cloud: Google
* Region: us-east1
* Subnet CIDR: 22
* Enable GKE: enabled
* Cluster Mode: GKE Standard

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption><p>Create Infrastructure with GKE Standard</p></figcaption></figure>

This takes about 20 minutes.  Infrastructure status should move to Completed. At the end of it, double-check that a "plan" (Administrators --> Plans) has been created with the same name (nonprod).

### View GKE Cluster details

You can view the details and download the kubeconfig file to connect the cluster from GKE Tab available in the infrastructure created.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (2).png" alt=""><figcaption><p>View GKE Standard Cluster</p></figcaption></figure>

