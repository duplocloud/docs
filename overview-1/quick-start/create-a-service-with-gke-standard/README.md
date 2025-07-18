---
description: Finish the Quick Start Tutorial by creating a Service using GKE Standard
---

# Create a Service with GKE Standard

In this tutorial for DuploCloud AWS, you have so far created a VPC network with configuration templates ([Infrastructure and Plan](../step-1-infrastructure.md)) and an isolated workspace ([Tenant](../step-2-tenant.md)).

Now you need to create a DuploCloud Service on top of your Infrastructure and configure the Service to run and deploy your application. In this tutorial path, we'll deploy using Docker containers, leveraging Google Cloud Platform's (GCE) Google Kubernetes Engine (GKE) Standard.

Alternatively, you can finish this tutorial by:

* [Creating a DuploCloud Service using GCE's GKE Autopilot.](broken-reference)&#x20;

For a comparison of the benefits of GKE Autopilot vs. GKE Standard, consult this [Google Cloud article](https://cloud.google.com/kubernetes-engine/docs/resources/autopilot-standard-feature-comparison).

_Estimated time to complete remaining tutorial steps: 30-40 minutes_

## Deploying a GKE Standard Service in DuploCloud

For the remaining steps in this tutorial, you will:&#x20;

1. Create a GCE Virtual Machine (VM) or a Node Pool.
2. Create a Service and applications (**webapp)** using the premade Docker image `nginx:latest.`
3. Expose the Service by creating and sharing a load balancer and DNS name.&#x20;
4. Test the application.
