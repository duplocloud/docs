# Step 1: Infrastructure

From the DuploCloud Portal, navigate to **Administrator** -> **Infrastructure**. Click **Add**. The **Add Infrastructure** page displays.&#x20;

Create an infrastructure with the following inputs:

* Name: nonprod
* Account: Google Cloud account
* VPC CIDR: 10.10.0.0/16
* Cloud: Google
* Region: us-east1
* Subnet CIDR: 22
* Enable GKE: enabled
* Cluster Mode: GKE Autopilot

<div align="left">

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-12 at 5.08.04 PM.png" alt=""><figcaption><p><strong>Add Infrastructure</strong> page</p></figcaption></figure>

</div>

Creating the Infrastructure takes approximately 20 minutes. Check your progress by monitoring the status column: the status will change from Pending to Complete when the Infrastructure is complete. When the infrastructure is complete, navigate to **Administrators** -> **Plans** and double-check that a "Plan" with the same name (nonprod) has been created.

<div align="left">

<figure><img src="../../.gitbook/assets/image (4) (1) (3).png" alt=""><figcaption></figcaption></figure>

</div>

### View GKE Cluster details

When an Infrastructure is created, a GKE Cluster is created by default. You can view the details and download the kubeconfig file from the DuploCloud portal.&#x20;

From the DuploCloud portal, navigate to **Administrator** -> **Infrastructure**. Click on the name of the Infrastructure, and select the **GKE** tab. To download the kubeconfig file, click **Download Kube Config**.

<div align="left">

<figure><img src="../../.gitbook/assets/image (23) (3).png" alt=""><figcaption></figcaption></figure>

</div>
