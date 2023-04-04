# Quick Start - EKS Services



This tutorial shows you how to set up an end-to-end cloud deployment for the sample topology shown below.

![Sample High Level Topology](<../../../.gitbook/assets/image (3) (1) (3).png>)

* We will use the Tenant and Infrastructure created as part of [Step1](../step-1-infrastructure.md) and [Step2](../step-2-tenant.md).
* We will deploy the docker containers by leveraging Kubernetes Cluster (AWS EKS)

Following will be DuploCloud mapping of the above topology into DuploCloud constructs.

## Deployment Steps

The steps involved in the setup will be:

1. Refer to the Infrastructure and Tenant created in earlier steps.
2. Create a Host (EC2 Instance) which will be an EKS worker
3. Create a MySQL RDS Database
4. Create a micro-service called **webapp** with the docker image `duplocloud/nodejs-hello:latest`
5. Expose the web app using a load balancer and a DNS name.&#x20;
6. Test the web app.
7. Obtain access to the container shell and `kubectl` for debugging.

## Network Architecture and Configurations

Behind the scenes, the topology that will get created will look like the following lower-level configuration in AWS.

<figure><img src="../../../.gitbook/assets/network-diagram.png" alt=""><figcaption><p>AWS architecture and configuration</p></figcaption></figure>

