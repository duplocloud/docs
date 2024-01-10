---
description: Key terms and concepts in DuploCloud AWS
---

# Key DuploCloud concepts

{% hint style="info" %}
The following concepts do not apply to ECS. ECS uses a proprietary policy model, which is explained in a [later section](../use-cases/disaster-recovery/ecs-setup/).
{% endhint %}

Familiarize yourself with these DuploCloud concepts and terms before deploying containerized applications in DuploCloud. See [use cases](../use-cases/) for a description of DuploCloud Infrastructures and Tenants.

* **Hosts**: These are virtual machines (EC2 Instances). For EKS deployments, they are also called Worker nodes. By default, apps within a Tenant are pinned to VMs in the same Tenant. In the case of EKS, we can deploy Hosts in one Tenant that can be leveraged by apps in other Tenants. This is called a shared-host model. This does not apply to ECS Fargate.
* **Service**: This is a DuploCloud terminology that is quite different from a "Kubernetes Service." A DuploCloud Service refers to a micro-service defined by a Name, DockerImage, number of replicas, and many other optional parameters. Behind the scenes, a DuploCloud Service maps 1:1 to a Deployment Set or a StatefulSet based on whether the microservice has stateful volumes. There are tons of optional Service configurations that represent various ways Docker containers can be run. A few of these are:
  * Environment variables
  * Host Network Mode
  * Volume mounts
  * Entry point or command overrides
  * Resource caps
  * Health Checks
* **Allocation Tags**: If a Service needs to be pinned to run only a specific set of Hosts, this can be achieved by setting a string on both the Hosts and Service. An Allocation Tag is a case-insensitive substring match (i.e. the Allocation Tag specified on the Service should be a substring of the tag specified on the Host). For example, if a Host is tagged as _HighCpu;HighMem_. a Service as tagged _highcpu_ can be allocated to this Host. However, if the Service is tagged _highcpu;gpu,_ then it can't, as this is not a substring of the Host's tag.
  * If a Service does not have any tags set, it can run on any Host.

{% hint style="info" %}
If a Host and Service are tagged with the same tag, that Host is also available for Services that have no tags. So the only way to assign a Host exclusively to a set of Services is to tag every Service in the Tenant with the same value.
{% endhint %}

For Kubernetes deployments, Allocation Tags are mapped to labels on nodes and then node selectors on the the _Deploymentset or Statefulset._

* **Host Networking:** By default, Docker containers have their own network addresses. But at times you may want them to use the same network interface as the VM. This is called Host Network Mode.

{% hint style="info" %}
{% code overflow="wrap" fullWidth="false" %}
```
Classic ELB can be used when the application is exposing non-HTTP ports and operating on any TCP port.
```
{% endcode %}
{% endhint %}

## Hosts

Hosts are virtual machines (VMs) (EC2 Instances). In EKS deployments, VMs are also known as Worker nodes. By default, apps within a Tenant are pinned to VMs in the same Tenant. In the case of EKS, you deploy Hosts in a separate Tenant. Applications in other Tenants can leverage these Hosts. This is called the shared host model. The shared host model does not apply to ECS Fargate.

## Service

Service is a DuploCloud term and is not the same as a Kubernetes Service. In DuploCloud, a Service is a micro-service defined by a Name, Docker Image, Number of Replicas, and many other optional parameters. Behind the scenes, a DuploCloud Service maps 1:1 to a DeploymentSet or a StatefulSet, based on whether the microservice has stateful volumes. There are many optional Service configurations representing various ways that Docker containers can be run. Among these are:

* Environment variables
* Host Network Mode
* Volume mounts
* Entrypoint or command overrides
* Resource caps
* Kubernetes health checks

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
