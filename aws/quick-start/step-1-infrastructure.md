# Step 1: Infrastructure

From the UI (Administrator --> Infrastructure) create an infrastructure with the following inputs:

* Name: non-prod
* Region: us-west-2
* VPC CIDR: 10.221.0.0/16
* Subnet CIDR Mask 24
* Availability Zones 2
* Enable EKS
* Enable ECS Cluster

This takes about 20 minutes. Kubernetes is the part that takes 15 minutes. Wait for the status to be completed. At the end of it, double check that a "plan" (Administrators--> Plans) has been created with the same name (non-prod).

If it has been more than 20 minutes then click on Faults (Administrator-->Faults) to see if there is an obvious error and if help is needed ping in the DuploCloud slack or teams channel.
