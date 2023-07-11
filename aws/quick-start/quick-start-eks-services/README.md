---
description: Finish the Quick Start Tutorial by creating an EKS Service
---

# Creating an EKS Service

In this tutorial for DuploCloud AWS, you have so far created a VPC instance with configuration templates ([Infrastructure and Plan](../step-1-infrastructure.md)), an isolated workspace ([Tenant](../step-2-tenant.md)), and optionally, an [RDS database instance](../step-4-create-a-rds-database.md).

Now you need to create a DuploCloud Service on top of your Infrastructure and configure the Service to run and deploy your application. In this tutorial path, we'll deploy using Docker containers, leveraging [AWS Elastic Kubernetes Service (EKS)](https://aws.amazon.com/eks/).&#x20;

Alternatively, you can finish this tutorial by:

* [Creating an AWS ECS Service in DuploCloud](../quick-start-ecs-services/) running Docker containers
* [Creating a DuploCloud native Docker Service](../quick-start-duplocloud-docker-services/)

For a full discussion of the benefits of EKS vs. ECS, consult[ this AWS blog](https://aws.amazon.com/blogs/containers/amazon-ecs-vs-amazon-eks-making-sense-of-aws-container-services/).

_Estimated time to complete remaining tutorial steps: 30-40 minutes_

## Deploying an AWS EKS Service in DuploCloud

For the remaining steps in this tutorial, you will:&#x20;

1. Create a Host (EC2 Instance), which serves as an [AWS EKS worker node](https://docs.aws.amazon.com/eks/latest/userguide/eks-compute.html).
2. Create a Service and applications (**webapp)** using the premade Docker image `duplocloud/nodejs-hello:latest.`
3. Expose the Service by creating and sharing a load balancer and DNS name.&#x20;
4. Test the application.
5. Obtain access to the container shell and `kubectl` for debugging.

## Network Architecture and Configurations

Behind the scenes, the topology that DuploCloud creates resembles this low-level configuration in AWS.

<figure><img src="../../../.gitbook/assets/network-diagram.png" alt=""><figcaption><p>AWS architecture and configuration</p></figcaption></figure>

