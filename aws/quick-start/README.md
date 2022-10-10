# Quick start

This tutorial shows you how to setup an end-to-end cloud deployment for the sample topology shown below.

![Sample High Level Topology](<../../.gitbook/assets/image (3) (1).png>)

* We will use nginx:latest as a sample for application container.
* We will create two environments or Tenants. One called Dev01 and other called QA01
* We will create a single Infrastructure (VPC) called non-prod in us-west-2 under which we will have both the tenants.
* We will deploy the docker containers by leveraging Kubernetes Cluster (AWS EKS)

Following will be DuploCloud mapping of the above topology into DuploCloud constructs.

The steps involved in the setup will be:

1. Create Infrastructure: This sets up the VPC, Subnets, NAT Gateway, Routes and Kubernetes Cluster.
2. Create a Tenant
3. Create an Host (EC2 Instance) which will be an EKS worker
4. Create a MySQL RDS Database
5. Create a micro-service called webapp with the docker image as nginx:latest
6. Expose the webapp using a loadbalancer and a DNS name. Test it
7. Enable central logging, metrics and alerts
8. Debugging capability like getting access to container shell, Kubectl and S3 AWS Console.
9. Finally we will import this setup into terraform and duplicate this into qa tenant using Terraform.

Behind the scenes the topology that will get created will look like the following lower level configuration in AWS. You are not really required to understand these details if you don't want to.

![](https://documents.lucid.app/documents/72886671-e5d7-48a9-90ab-c17df2554f63/pages/0\_0?a=1274\&x=59\&y=128\&w=1782\&h=1144\&store=1\&accept=image%2F\*\&auth=LCA%20fe1f1dee488c25d97f5dd501fc62605eda6d8d8d-ts%3D1647140256)
