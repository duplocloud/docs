---
description: Orchestration across multiple Cloud providers
---

# Container deployments

Most workloads deployed on DuploCloud are in Docker containers. The rest consist of serverless functions, Amazon EMR jobs, and SageMaker.&#x20;

DuploCloud supports virtually all orchestration techniques across multiple cloud providers using a simplified, cloud-neutral interface. On AWS, DuploCloud supports orchestration using Elastic Kubernetes Service (EKS) and Elastic Container Service (ECS) Fargate, and native Docker Containers.

In addition, the DuploCloud platform has a built-in container management platform that provides an alternative to Kubernetes, which can be complex to implement.  &#x20;

DuploCloud supports many types of applications in AWS, including but not limited to:

* Dockerized apps constitute about 90% of our user workloads. The platform orchestrates containerized application deployments using Docker, EKS, ECS, or built-in container orchestrations as defined in the [Container orchestration features](../../gcp/container-deployments/container-orchestrators.md) section.
* Sagemaker
* Glue&#x20;
