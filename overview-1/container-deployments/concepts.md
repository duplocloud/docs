---
description: Key concepts for using DuploCloud with Docker and GCP
---

# Key DuploCloud concepts

While deploying Dockerized applications, familiarize yourself with some key concepts and terminologies.

## Hosts

These are virtual machines. In GCP deployments, they are also called Worker nodes. By default, apps within a Tenant are pinned to VMs in the same Tenant. DuploCloud has the ability to deploy Hosts in a separate Tenant and apps in other Tenants that leverage these Hosts. This is called Shared Host Model and is not applicable to GCP.

## Services

Service is a DuploCloud term. DuploCloud Services are not Kubernetes Services. Services are microservices that are defined by a Name, Docker Image, and a number of replicas in addition to many other optional parameters. Behind the scenes, a DuploCloud Service maps 1:1 either to a Kubernetes deployment set or to a StatefulSet depending on whether the microservice has stateful volumes or not.

When deploying services, especially in a staging environment, it's crucial to ensure that containers have the necessary permissions for read/write operations. This may involve configuring a security context within the service's configuration to address local write failures, a common issue when containers are restricted compared to their local development environment. This adjustment ensures that the container can write to temporary file directories on the server, facilitating smooth deployment and operation.

Services have many optional configurations representing various ways Docker containers can be run, including:

* Environment variables
* Host Network Mode
* Volume mounts
* Entrypoint or command overrides
* Resource caps
* Health Checks

## Allocation Tags

Allocation tags allow you to control which Hosts a Service can run on by specifying tags on both the Host and the Service. Services without allocation tags can be scheduled on any Host.

* Docker Services use case-insensitive, substring-based matching.\
  For example, if a Host has the tag `HighCpu;HighMem`, a Service tagged `highcpu` or `cpu` would match and be eligible to run on that Host.
* Kubernetes Deployments use exact, case-sensitive matching based on Kubernetes node labels and node selectors. For example, a Host tagged `frontend-prod` will only match a Service with the exact same tag: `Frontend-Prod` or `frontend-prod-1` will **not** match. Kubernetes allocation tags must start and end with an alphanumeric character and may only contain letters, numbers, hyphens (`-`), or periods (`.`)

If a Host is tagged and a matching Service exists, the Host may still be used by untagged Services unless all Services in the tenant are tagged. To fully isolate Hosts for a specific purpose, ensure **all** Services use allocation tags.

## **Host Networking**

By default, Docker containers have their own network addresses. If you want these containers to use the same network interface as the underlying VM, you must use Host Network Mode.

## **Load Balancers**

&#x20;If a Service must be accessed by other Services, it needs to be exposed using internal and external Load Balancers.

This comprehensive approach ensures that services are deployed efficiently and securely, with appropriate configurations for networking, permissions, and resource allocation, facilitating a smooth operation across different environments.
