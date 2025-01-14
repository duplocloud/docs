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

If a service needs to be pinned to run only a specific set of Hosts, set an Allocation Tag on the Hosts as well as on the Service. The Allocation Tag is a case-insensitive substring match in case of Docker native deployments and exact match in case of Kubernetes deployments. For example, an Allocation Tag specified on a Docker native Service is usually a substring of the tag specified on the Host. If a Host is tagged **HighCpu;HighMem,** a Service tagged **highcpu** can be allocated on it. However, if the Service is tagged **highcpu;gpu** then it won't be allocated; it would need a Host tagged **highcpu;gpu**_._ If a Service does not have any tag set, it can be placed on any Host.

{% hint style="warning" %}
If the Host is tagged with a specific value and you have Services with the same tag, the Host is available for any Service that has no tags. If you want the exclusive assignment of a Host to a set of Services, ensure that every Service in the Tenant is tagged with some value.
{% endhint %}

In the case of Kubernetes deployments, the concept of Allocation Tags maps to labels on nodes, and on node selectors on the deployment set or StatefulSet. **The allocation tag on the service must exactly match  the allocation tag (label) on the node/node pool.**

{% hint style="info" %}
In Kubernetes deployments, allocation tags must start and end with alphanumeric characters. The only supported special characters are the period (.) and hyphen (-). For example, **highmem.highcpu is** is a valid allocation tag, but **highmem;highcpu** is not.
{% endhint %}



* **Host Networking:** By default, Docker containers have their own network addresses. you may want these containers to use the same network interface as the VM. This is called Host Network Mode.
* **Load Balancer:** If a service must be accessed by other services, it needs to be exposed using a Load Balancer. Supported Load Balancers include:&#x20;
  * A Network Load Balancer (NLB). An NLB distributes traffic across several servers by using the TCP/IP networking protocol. By combining two or more computers that are running applications into a single virtual cluster, NLB provides reliability and performance for web servers and other mission-critical servers.
  * An Application Load Balancer (ALB). An ALB provides outbound connections to cluster nodes inside the AKS virtual network, translating the private IP address to a public IP address as part of its Outbound Pool.
