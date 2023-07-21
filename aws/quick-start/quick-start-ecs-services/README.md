# Creating an ECS Service

In this guide, we will deploy a web application using ECS Fargate.

The steps involved in the setup will be:

* Use the Infrastructure created in [Step1](../step-1-infrastructure.md) and [Step2 ](../step-2-tenant.md)in the quickstart guide.
* Create a Task Definition.
* Create a micro-service called `webapp` with the Docker image as `nginx:latest`
* Expose the web app using a load balancer and test it.
