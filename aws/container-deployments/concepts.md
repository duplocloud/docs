---
description: Key terms and concepts in DuploCloud AWS
---

# Key DuploCloud concepts

{% hint style="info" %}
The following concepts do not apply to ECS. ECS uses a proprietary policy model, which is explained in a [later section](../use-cases/disaster-recovery/ecs-initial-setup.md).
{% endhint %}

While deploying containerized applications in DuploCloud, be familiar with these DuploCloud concepts and terms. See [Use Cases](../use-cases/) for a description of DuploCloud Infrastructures and Tenants.

* **Hosts**: These are virtual machines (EC2 Instances). In case of EKS deployments they are also called Worker nodes. By default apps within a tenant are pinned to VMs in the same Tenant. In case of EKS we have the ability to deploy Hosts in a separate tenant and apps in other tenants can leverage these hosts. This is called the shared host model.\
  This is not applicable to ECS Fargate.
* **Service**: This is a DuploCloud terminology and is not to be confused with "Kubernetes Service". This represents a micro-service defined by a Name, DockerImage and number of replicas in addition to many other optional parameters. Behind the scenes, a DuploCloud Service maps 1:1 either to a DeploymentSet or to a StatefulSet based on whether the microservice has stateful volumes or not. There are tons of optional configurations associated with a service that represent various ways a docker containers can be run. A few of these are
  * Environment variables
  * Host Network Mode
  * Volume mounts
  * Entrypoint or command overrides
  * Resource caps
  * Health Checks
* **Allocation Tags**: If a service needs to be pinned to run only a specific set of hosts this can be achieved by setting a string on both the hosts as well as the Service. Allocation Tag is a case-insensitive substring match i.e. Allocation Tag specified on a service should be a substring of the tag specified on the host. For example a Host maybe tagged as _HighCpu;HighMem_ and the service if tagged _highcpu_ can be allocated on this host. But if the service is tagged _highcpu;gpu_ then it won't be as it needs a host that has _highcpu;gpu_ where
  * If a service does not have any tag set then it can be placed on any host.

{% hint style="info" %}
If the host is tagged with a specific value and you have services with same tag even then the host is available for any service which has **no tags.** So if you want exclusive assignment of a host to a set of services only then the only way of achieving this is to make sure every service in the tenant is tagged with some value.
{% endhint %}

In case of Kubernetes deployments the concept of allocation tags is realized by mapping it to labels on nodes and then node selector on the _Deploymentset or Statefulset_

* **Host Networking:** By default Docker containers have their own network addresses. But at times it is desirable that these containers could reuse the same network interface as the VM itself. This is called Host Network Mode.

{% hint style="info" %}
```
Classic ELB can be used when the application is exposing non HTTP ports and operating on any TCP port.
```
{% endhint %}

## Hosts

_Hosts_ are virtual machines (VMs) (EC2 Instances). In EKS deployments, VMs are also known as _Worker nodes_. By default, apps within a tenant are pinned to VMs in the same Tenant. In the case of EKS, you deploy Hosts in a separate Tenant. Applications in other tenants can leverage these hosts. This is called the _shared host model_. The shared host model is not applicable to ECS Fargate.

## Service

_Service_ is a DuploCloud term and is not the same as a Kubernetes Service. In DuploCloud, a Service is a micro-service defined by a **Name**, Docker **Image,** and **Number of Replicas**, in addition to many other optional parameters. Behind the scenes, a DuploCloud Service maps 1:1 either to a DeploymentSet or to a StatefulSet, based on whether or not the microservice has stateful volumes. There are many optional configurations associated with a service, representing various ways that docker containers can be run. Among these are:

* Environment variables
* Host Network Mode
* Volume mounts
* Entrypoint or command overrides
* Resource caps
* Kubernetes Health Checks

## Allocation Tags

If a service needs to be pinned to run only a specific set of hosts, you set an _Allocation Tag_ on both the hosts, as well as the Service. Allocation Tags are case-insensitive substrings. Allocation Tags on a service should be a substring of the tag specified on the host. For example, if a Host is tagged as _**HighCpu;HighMem**_, then the service (if it is tagged _**highcpu**)_ can be allocated on this host. If a service does not have any tag set, it can be placed on any host.

{% hint style="info" %}
If the host is tagged with a specific value, and you have services with the same tag, the host is available for any service which has no tags**.** If you want the exclusive assignment of a host to a set of services, ensure every service in the Tenant is tagged.
{% endhint %}

For Kubernetes deployments the concept of allocation tags is realized by mapping it to labels on nodes and then node selector on the _Deploymentset or Statefulset_

## Host Networking

By default, Docker containers have their network addresses. At times, you may want these containers to reuse the same network interface that the VM uses. This reuse is called _Host Network Mode_.

## Load Balancer

Every DuploCloud Service that communicates with other Services, needs to be exposed by a LoadBalancer. DuploCloud supports the following Load Balancers (LBs).

* **Application Elastic Load Balancer (ELB)**: When exposed by an ELB, the DuploCloud Service is reachable from anywhere unless it is marked as **Internal**, in which case it is reachable only from within the VPC (or DuploCloud Infrastructure). Application ELBs allow you to use a certificate for terminating SSL on the LB, which allows you to avoid providing application SSLs and certificates, such as a certificate issued from [AWS Amazon Certificate Manager (ACM](https://aws.amazon.com/certificate-manager/)).\
  In Kubernetes, the platform creates a [NodePort ](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)pointing to the DeploymentSet and adds the Host IPs of the worker nodes to the ELB. Traffic flows from the client to the external port defined in the ELB (for example, 443), to the ELB's NodePort (for example, 30004 on the Worker Node), and to the Kubernetes Proxy running on each Worker Node. The Worker Node forwards the NodePort to the container.&#x20;
* **Classic ELB (Only applicable to Built-In Container Orchestration)**: Classic ELBs can be used when the application is exposing non-HTTP ports and they operate on any TCP port. When exposed by an ELB, the Service is reachable from anywhere unless it is marked as **Internal**, in which case it is reachable only from within the VPC (or DuploCloud infrastructure). Classic ELBs allow you to use a certificate for terminating SSL on the LB. which allows you to avoid providing application SSLs and certificates, such as a certificate issued from [AWS Amazon Certificate Manager (ACM](https://aws.amazon.com/certificate-manager/)).&#x20;

* Cluster IP (Kubernetes only): [Kubernetes ClusterIP](https://kubernetes.io/docs/concepts/services-networking/service/#type-clusterip) load balancers can be used if you are required to expose the application only within the Kubernetes Cluster.
