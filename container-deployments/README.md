# Container Deployments

Most application workloads deployed on DuploCloud are in Docker containers. The rest consist of serverless functions, Big data workloads like Amazon EMR jobs, Airflow and SageMaker.&#x20;

DuploCloud supports virtually all orchestration techniques across multiple cloud providers using a simplified, cloud-neutral interface. On AWS, DuploCloud supports orchestration using Elastic Kubernetes Service (EKS) and Elastic Container Service (ECS) Fargate. One GCP we support GKE auto pilot and node pool based. On Azure we support AKS and Azure web apps.

In addition, the DuploCloud platform has a built-in container management platform that we call "Docker Native" and provides an alternative to Kubernetes. This is for smaller workloads where Kubernetes can be an overkill.  &#x20;

