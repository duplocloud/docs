---
description: >-
  Get up and running with DuploCloud inside an AWS cloud environment; harness
  the power of generating application infrastructures.
---

# AWS Quick Start

This Quick Start tutorial shows you how to set up an end-to-end cloud deployment. You will create AWS infrastructure and tenants and, by the end of this tutorial, you can view a deployed sample web application.

_Estimated time to complete tutorial: 75-95 minutes._

## AWS Tutorial Roadmap

When you complete the AWS Quick Start Tutorial, you have three options or paths, as shown in the table below.

* Using EKS - You create a service in DuploCloud using AWS Elastic Kubernetes Service and expose it using a load balancer within DuploCloud.
* Using ECS - You create an app and service in DuploCloud using AWS Elastic Container Service.
* Using Native Docker Services - You create a service in Docker and expose it using a load balancer within DuploCloud.

{% hint style="info" %}
There are optional steps in each tutorial path, in the table below, marked with an asterisk. While these steps are unnecessary to complete each tutorial, you may want to perform or read through them, as they are tasks normally completed when you create production-ready services.
{% endhint %}

For information about the differences between these methods, to help you choose which method best suits your needs, skills, and environments, see this [AWS blog](https://aws.amazon.com/blogs/containers/amazon-ecs-vs-amazon-eks-making-sense-of-aws-container-services/) and the [Docker ](https://docs.docker.com/)documentation.

<table data-full-width="false"><thead><tr><th width="85">Step</th><th>EKS</th><th>ECS</th><th width="217">Native Docker Services</th></tr></thead><tbody><tr><td>1</td><td>Create Infrastructure and Plan</td><td>Create Infrastructure and Plan</td><td>Create Infrastructure and Plan</td></tr><tr><td>2</td><td>Create Tenant</td><td>Create Tenant</td><td>Create Tenant</td></tr><tr><td>3</td><td>Create RDS *</td><td>Create RDS *</td><td>Create RDS *</td></tr><tr><td>4</td><td>Create Host</td><td>Create a Task Definition for an application</td><td>Create Host</td></tr><tr><td>5</td><td>Create Service</td><td>Create the ECS Service and Load Balancer</td><td>Create app</td></tr><tr><td>6</td><td>Create Load Balancer</td><td>Test the app</td><td>Create Load Balancer</td></tr><tr><td>7</td><td>Enable Load Balancer Options *</td><td></td><td>Test the App</td></tr><tr><td>8</td><td>Create Custom DNS Name *</td><td></td><td></td></tr><tr><td>9</td><td>Test the App</td><td></td><td></td></tr></tbody></table>

\* - Optional Step

## AWS Video demo

Click the card below to open the DuploCloud video page to watch a number of DuploCloud demos.

{% embed url="https://duplocloud.com/videos/" %}
DuploCloud video demos
{% endembed %}

