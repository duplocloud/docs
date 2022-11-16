# QuickStart - EKS Services



This tutorial shows you how to setup an end-to-end cloud deployment for the sample topology shown below.

![Sample High Level Topology](<../../../.gitbook/assets/image (3) (1) (3).png>)

* We will use the Tenant and Infrastructure created as part of [Step1](../step-1-infrastructure.md) and [Step2](../step-2-tenant.md).
* We will deploy the docker containers by leveraging Kubernetes Cluster (AWS EKS)

Following will be DuploCloud mapping of the above topology into DuploCloud constructs.

## Deployment Steps

The steps involved in the setup will be:

1. Refer the Infrastructure and Tenant created in earlier steps.
2. Create an Host (EC2 Instance) which will be an EKS worker
3. Create a MySQL RDS Database
4. Create a micro-service called webapp with the docker image as duplocloud/nodejs-hello:latest
5. Expose the webapp using a loadbalancer and a DNS name. Test it
6. Debugging capability like getting access to container shell and Kubectl

## Network Architecture and Configurations

Behind the scenes the topology that will get created will look like the following lower level configuration in AWS.

![](https://documents.lucid.app/documents/72886671-e5d7-48a9-90ab-c17df2554f63/pages/0\_0?a=1274\&x=59\&y=128\&w=1782\&h=1144\&store=1\&accept=image%2F\*\&auth=LCA%20fe1f1dee488c25d97f5dd501fc62605eda6d8d8d-ts%3D1647140256)
