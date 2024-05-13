---
description: Key concepts for using DuploCloud with Docker and GCP
---

# Key DuploCloud concepts

While deploying Dockerized applications, familiarize yourself with some key concepts and terminologies.

## Hosts

These are virtual machines. In GCP deployments, they are also called Worker nodes. By default, apps within a Tenant are pinned to VMs in the same Tenant. DuploCloud has the ability to deploy Hosts in a separate Tenant and apps in other Tenants that leverage these Hosts. This is called Shared Host Model and is not applicable to GCP.

## Service

Service is a DuploCloud term. DuploCloud Services are not Kubernetes Services. Services are microservices that are defined by a Name, DockerImage, and a number of replicas in addition to many other optional parameters. Behind the scenes, a DuploCloud Service maps 1:1 either to a Kubernetes deployment set or to a StatefulSet depending on whether the microservice has stateful volumes or not. There are many optional configurations associated with a DuploCloud Service that represent various ways Docker containers can be run. A few of these are:

* Environment variables&#x20;
* Host Network Mode&#x20;
* Volume mounts&#x20;
* Entrypoint or command overrides&#x20;
* Resource caps&#x20;
* Health Checks

## Allocation Tags

If a service needs to be pinned to run only a specific set of hosts, set an Allocation Tag on the Hosts as well as on the Service. The Allocation Tag is a case-insensitive substring match. For example, an Allocation Tag specified on a service is usually a substring of the tag specified on the host. A Host may be tagged as **HighCpu;HighMem** and the Service (if tagged **highcpu**) can be allocated on the Host. However, if the service is tagged **highcpu;gpu** then it won't be allocated and needs a host that has been tagged **highcpu;gpu**_._ If a Service does not have any tag set, it can be placed on any host.

{% hint style="warning" %}
If the Host is tagged with a specific value and you have Services with the same tag, the host is available for any Service which has no tags. If you want the exclusive assignment of a Host to a set of Services, ensure that every Service in the Tenant is tagged with some value.
{% endhint %}

In the case of Kubernetes deployments, the concept of Allocation Tags maps to labels on nodes, and on node selectors on the deployment set or StatefulSet.

* **Host Networking:** By default, Docker containers have their own network addresses. you may want these containers to use the same network interface as the VM. This is called Host Network Mode.
* **Load Balancer:** If a service must be accessed by other services, it needs to be exposed using internal and external load balancers.&#x20;
