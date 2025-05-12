---
description: Key concepts for using DuploCloud with Docker and Azure
---

# Key DuploCloud concepts

While deploying Dockerized applications, familiarize yourself with some key concepts and terminologies.

See [Use Cases](../use-cases/) for a description of DuploCloud Infrastructures and Tenants.

## Hosts

These are virtual machines. In AKS deployments, they are also called Worker nodes. By default, apps within a Tenant are pinned to VMs in the same Tenant.&#x20;

## Service

Service is a DuploCloud term. DuploCloud Services are not Kubernetes Services. Services are microservices that are defined by a Name, DockerImage, and number of replicas in addition to many other optional parameters. Behind the scenes, a DuploCloud Service maps 1:1 either to a Kubernetes deployment set or to a StatefulSet depending on whether the microservice has stateful volumes or not. There are many optional configurations associated with a DuploCloud Service that represent various ways Docker containers can be run. A few of these are:

* Environment variables&#x20;
* Host Network Mode&#x20;
* Volume mounts&#x20;
* Entrypoint or command overrides&#x20;
* Resource caps&#x20;
* Health Checks

## Allocation Tags

Allocation tags allow you to control which Hosts a Service can run on by specifying tags on both the Host and the Service. Services without allocation tags can be scheduled on any Host.

* Docker Services use case-insensitive, substring-based matching.\
  For example, if a Host has the tag `HighCpu;HighMem`, a Service tagged `highcpu` or `cpu` would match and be eligible to run on that Host.
* Kubernetes Deployments use exact, case-sensitive matching based on Kubernetes node labels and node selectors. For example, a Host tagged `frontend-prod` will only match a Service with the exact same tag: `Frontend-Prod` or `frontend-prod-1` will not match. Kubernetes allocation tags must start and end with an alphanumeric character and may only contain letters, numbers, hyphens (`-`), or periods (`.`)

If a Host is tagged and a matching Service exists, the Host may still be used by untagged Services unless all Services in the tenant are tagged. To fully isolate Hosts for a specific purpose, ensure **all** Services use allocation tags.

## **Host Networking**

By default, Docker containers have their own network addresses. you may want these containers to use the same network interface as the VM. This is called Host Network Mode.

## **Load Balancers**

If a service must be accessed by other services, it needs to be exposed using a Load Balancer. Supported Load Balancers include:

* A Network Load Balancer (NLB). An NLB distributes traffic across several servers by using the TCP/IP networking protocol. By combining two or more computers that are running applications into a single virtual cluster, NLB provides reliability and performance for web servers and other mission-critical servers.
* An Application Load Balancer (ALB). An ALB provides outbound connections to cluster nodes inside the AKS virtual network, translating the private IP address to a public IP address as part of its Outbound Pool.
