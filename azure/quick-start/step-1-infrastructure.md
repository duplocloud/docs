# Step 1: Infrastructure

From the DuploCloud Portal (Administrator --> Infrastructure) create an infrastructure with the following inputs:

* Name: nonprod
* Subscription: Select Azure Subscription from the dropdown
* VPC CIDR: 10.23.0.0/16
* Subnet CIDR: 10.23.0.0/20
* Cloud: Azure

![Infrastructure Creation](<../../.gitbook/assets/image (44) (1).png>)

This takes about 20 minutes.  Infrastructure status should move to Completed. At the end of it, double check that a "plan" (Administrators --> Plans) has been created with the same name (nonprod).

![Infrastructure creation complete](<../../.gitbook/assets/image (30) (1).png>)

If it has been more than 20 minutes, click on Faults (Administrator--> Faults) to see if there is an obvious error and if help is needed ping in the DuploCloud slack or teams channel.

### Enable AKS Kubernetes Cluster in Infrastructure

View the Infrastructure created in the above step. Goto **Kubernetes** Tab and **Enable  the Kubernetes Cluster.** Details of the Kubernetes Cluster is listed under Kubernetes Tab.

![Kubernetes details](<../../.gitbook/assets/image (38) (3).png>)

