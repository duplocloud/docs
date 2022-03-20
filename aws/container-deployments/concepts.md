# Concepts

While deploying Dockerized applications, here are a few concepts and terminologies to be aware of

* **Hosts**: These are virtual machines (EC2 Instances). In case of EKS deployments they are also called Worker nodes. By default apps within a tenant are pinned to VMs in the same Tenant. In case of EKS we have the ability to deploy Hosts in a separate tenant and apps in other tenants can leverage these hosts. This is called the shared host model.  \
  This is not applicable to ECS Fargate.
* **Service**: This is a DuploCloud terminology and is not to be confused with "Kubernetes Service". This represents a micro-service defined by a Name, DockerImage and number of replicas in additional to many other optional parameters. Behind the scenes, a DuploCloud Service maps 1:1 either a DeploymentSet or StatefulSet based on wether the microservice has stateful volumes or not. There are tons are optional configurations associated with a service which represents various ways a docker containers can be run. A few of these are
  * Environment variables
  * Volume mounts
  * Entrypoint or command overrides
  * Resource caps  &#x20;
