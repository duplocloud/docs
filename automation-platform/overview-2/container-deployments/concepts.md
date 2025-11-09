---
description: Key concepts for using DuploCloud with Docker and Azure
---

# Key DuploCloud Concepts

Familiarize yourself with some key concepts and terminologies.

For descriptions of other common DuploCloud concepts, like Infrastructures and Tenants, see the [Common Components documentation](../../../introduction/application-focused-interface-duplocloud-architecture/duplocloud-common-components/).

## Hosts

These are virtual machines. In AKS deployments, they are also called Worker nodes. By default, apps within a Tenant are pinned to VMs in the same Tenant.&#x20;

## Services

Service is a DuploCloud term. DuploCloud Services are not Kubernetes Services. Services are microservices defined by a Name, Docker image, number of replicas, and other optional parameters. Behind the scenes, a DuploCloud Service maps 1:1 either to a Kubernetes deployment set or to a StatefulSet, depending on whether it has stateful volumes. Optional configurations represent various ways Docker containers can be run, such as:

* Environment variables&#x20;
* Host Network Mode&#x20;
* Volume mounts&#x20;
* Entrypoint or command overrides&#x20;
* Resource caps&#x20;
* Health Checks

If a service needs to be pinned to run only on a specific set of Hosts, set an Allocation Tag on the Hosts as well as on the Service. The Allocation Tag is a case-insensitive substring match in case of Docker native deployments and exact match in case of Kubernetes deployments. For example, an Allocation Tag specified on a Docker native Service is usually a substring of the tag specified on the Host. If a Host is tagged **HighCpu;HighMem,** a Service tagged **highcpu** can be allocated on it. However, if the Service is tagged **highcpu;gpu** then it won't be allocated; it would need a Host tagged **highcpu;gpu**_._ If a Service does not have any tag set, it can be placed on any Host.

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
