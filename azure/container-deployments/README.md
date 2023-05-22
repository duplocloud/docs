---
description: Orchestration across multiple Cloud providers
---

# Container deployments

The majority of workloads deployed on DuploCloud are in Docker containers.&#x20;

DuploCloud supports virtually all orchestration techniques across multiple cloud providers, using a simplified and cloud-neutral interface. Orchestration includes support for Elastic Kubernetes Service (EKS) and Elastic Container Service (ECS) on AWS, Managed Kubernetes Service (AKS), WebApps in Azure, Google Kubernetes Engine (GKE) on GCP, and Oracle Kubernetes in Red Hat OpenShift Container Platform (OCP).&#x20;

In addition, the DuploCloud platform has a built-in container management platform that provides an alternative to Kubernetes, which can be complex to implement.  &#x20;

DuploCloud supports many types of applications in Azure, including but not limited to:

* [Dockerized apps](../../aws/container-deployments/) constitute about 90% of our user workloads. The platform orchestrates containerized application deployments using AKS or built-in container orchestrations as defined in the [Container orchestration features](../../gcp/container-deployments/container-orchestrators.md) section.
* Sagemaker
* Glue&#x20;

{% hint style="info" %}
If you need other services, please get in touch with your DuploCloud support team. The typical turnaround time for creating a custom service is a business week.&#x20;
{% endhint %}
