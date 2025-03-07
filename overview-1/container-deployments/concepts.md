---
description: Key concepts for using DuploCloud with Docker and GCP
---

# Key DuploCloud concepts

While deploying Dockerized applications, familiarize yourself with some key concepts and terminologies.

## Hosts

These are virtual machines. In GCP deployments, they are also called Worker nodes. By default, apps within a Tenant are pinned to VMs in the same Tenant. DuploCloud has the ability to deploy Hosts in a separate Tenant and apps in other Tenants that leverage these Hosts. This is called Shared Host Model and is not applicable to GCP.

## Service

Service is a DuploCloud term. DuploCloud Services are not Kubernetes Services. Services are microservices that are defined by a Name, DockerImage, and a number of replicas in addition to many other optional parameters. Behind the scenes, a DuploCloud Service maps 1:1 either to a Kubernetes deployment set or to a StatefulSet depending on whether the microservice has stateful volumes or not.

When deploying services, especially in a staging environment, it's crucial to ensure that containers have the necessary permissions for read/write operations. This may involve configuring a security context within the service's configuration to address local write failures, a common issue when containers are restricted compared to their local development environment. This adjustment ensures that the container can write to temporary file directories on the server, facilitating smooth deployment and operation.

Services have many optional configurations representing various ways Docker containers can be run, including:

* Environment variables
* Host Network Mode
* Volume mounts
* Entrypoint or command overrides
* Resource caps
* Health Checks

## Allocation Tags

If a service needs to be pinned to run only a specific set of hosts, set an Allocation Tag on the Hosts as well as on the Service. The Allocation Tag is a case-insensitive substring match in case of Docker native deployments and case-insensitive exact match in case of Kubernetes deployments. For example, an Allocation Tag specified on a service is usually a substring of the tag specified on the host. A Host may be tagged as **HighCpu;HighMem** and the Service (if tagged **highcpu**) can be allocated on the Host on Docker native. However, if the service on Docker Native is tagged **highcpu;gpu** then it won't be allocated and needs a host that has been tagged **highcpu;gpu**. If a Service does not have any tag set, it can be placed on any host.

{% hint style="warning" %}
If the Host is tagged with a specific value and you have Services with the same tag, the host is available for any Service which has no tags. If you want the exclusive assignment of a Host to a set of Services, ensure that every Service in the Tenant is tagged with some value.
{% endhint %}

In the case of Kubernetes deployments, the concept of Allocation Tags maps to labels on nodes, and on node selectors on the deployment set or StatefulSet. **The allocation tag on the service must match exactly with the allocation tag on the node/node pool.**&#x20;

{% hint style="info" %}
In Kubernetes deployments, allocation tags must start and end with alphanumeric characters. The only supported special characters are the period (.) and hyphen (-). For example, **highmem.highcpu is** is a valid allocation tag, but **highmem;highcpu** is not.
{% endhint %}



* **Host Networking:** By default, Docker containers have their own network addresses. If you want these containers to use the same network interface as the VM, this is achieved through Host Network Mode.
* **Load Balancer:** If a service must be accessed by other services, it needs to be exposed using internal and external load balancers.

This comprehensive approach ensures that services are deployed efficiently and securely, with appropriate configurations for networking, permissions, and resource allocation, facilitating a smooth operation across different environments.
