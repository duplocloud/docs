# Step 1: Infrastructure

From the DuploCloud Portal (Administrator --> Infrastructure) create an infrastructure with the following inputs:

* Name: nonprod
* Account: Google Cloud account
* VPC CIDR: 10.10.0.0/16
* Cloud: Google
* Region: us-east1
* Subnet CIDR: 22
* Enable GKE: enabled

<figure><img src="../../.gitbook/assets/image (6) (3).png" alt=""><figcaption></figcaption></figure>

This takes about 20 minutes.  Infrastructure status should move to Completed. At the end of it, double-check that a "plan" (Administrators --> Plans) has been created with the same name (nonprod).

<figure><img src="../../.gitbook/assets/image (4) (4).png" alt=""><figcaption></figcaption></figure>

### View GKE Cluster details

By default when Infrastructure is created, GKE Cluster is created. You can view the details and download the kubeconfig file to connect the cluster from GKE Tab available in the infrastructure created.

<figure><img src="../../.gitbook/assets/image (23) (3).png" alt=""><figcaption></figcaption></figure>
