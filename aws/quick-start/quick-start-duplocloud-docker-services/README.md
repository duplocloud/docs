---
description: Finish the Quick Start Tutorial by running a native Docker Service
---

# Creating a Native Docker Service

This section of the tutorial shows you how to deploy a web application with a DuploCloud Docker Service, by leveraging DuploCloud platform in-built container management capability. &#x20;

{% hint style="info" %}
Instead of creating a DuploCloud Docker Service, you can alternatively finish the tutorial by:

* [Creating an AWS EKS Service in DuploCloud](../quick-start-eks-services/) running Docker containers or
* [Creating an AWS ECS Service in DuploCloud](../quick-start-ecs-services/) running Docker containers.
{% endhint %}

## Deploying a DuploCloud Docker Service

Instead of creating a DuploCloud service using EKS or ECS, you can deploy your application with native Docker containers and services and DuploCloud.&#x20;

To deploy your app with a DuploCloud Docker Service in this tutorial, you:&#x20;

1. Create an EC2 host instance in DuploCloud.
2. Create a native Docker application and service.
3. Expose the app to the web with an Application Load Balancer in DuploCloud.
4. Complete the tutorial by testing your application.

_Estimated time to complete remaining tutorial steps: 30-40 minutes_

## Network Architecture and Configurations

Behind the scenes, the topology that DuploCloud creates resembles this low-level configuration in AWS.

<figure><img src="../../../.gitbook/assets/image (3) (2) (2).png" alt=""><figcaption><p>DuploCloud Docker Service topology</p></figcaption></figure>
