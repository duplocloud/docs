---
description: Key terms and concepts in DuploCloud container orchestration
---

# Terminologies in Container Orchestration

{% hint style="info" %}
The following concepts do not apply to ECS. ECS uses a proprietary policy model, which is explained in a [later section](../overview/use-cases/creating-an-infrastructure-and-plan-for-aws/ecs-setup/).
{% endhint %}

Familiarize yourself with these DuploCloud concepts and terms before deploying containerized applications in DuploCloud. See the [DuploCloud Common Concepts](../welcome-to-duplocloud/application-focussed-interface/duplocloud-common-components/) section for a description of DuploCloud Infrastructures, Tenants, Hosts, and Services.

## Container Orchestration Terms

### Hosts

These are virtual machines (EC2 Instances, GCP Node pools, or Azure Agent Pools). By default, apps within a Tenant are pinned to VMs in the same Tenant. One can also deploy Hosts in one Tenant that can be leveraged by apps in other Tenants. This is called the shared-host model. The shared-host model does not apply to ECS Fargate.

### Services

Service is a DuploCloud term and is not the same as a Kubernetes Service. In DuploCloud, a Service is a micro-service defined by a name, Docker Image, number of replicas, and other optional parameters. Behind the scenes, a DuploCloud Service maps 1:1 to a Deployment or StatefulSet, based on whether it has stateful volumes. There are many optional Service configurations for Docker containers. Among these are:

* Environment variables
* Host Network Mode
* Volume mounts
* Entrypoint or command overrides
* Resource caps
* Kubernetes health checks

### Allocation Tags

Allocation tags allow you to control which Hosts a Service can run on by specifying tags on both the Host and the Service. Services without allocation tags can be scheduled on any Host.

* **Docker Services** use **case-insensitive, substring-based matching**.\
  For example, if a Host has the tag `HighCpu;HighMem`, a Service tagged `highcpu` or `cpu` would match and be eligible to run on that Host.
* **Kubernetes Deployments** use **exact, case-sensitive matching** based on Kubernetes node labels and node selectors. For example, a Host tagged `frontend-prod` will only match a Service with the exact same tag. For example `Frontend-Prod` or `frontend-prod-1` will **not** match. Kubernetes allocation tags must start and end with an alphanumeric character and may only contain letters, numbers, hyphens (`-`), or periods (`.`)

If a Host is tagged and a matching Service exists, the Host may still be used by untagged Services unless **all Services in the tenant are tagged**. To fully isolate Hosts for a specific purpose, ensure **all** Services use allocation tags.

### Host Networking

By default, Docker containers have network addresses. Sometimes, containers share the VM network interface. This reuse is called host networking mode.

### Load Balancer

A DuploCloud Service that communicates with other Services, must be exposed by a Load Balancer. DuploCloud supports the following Load Balancers (LBs).

#### **Application Elastic Load Balancer (ELB)**

A DuploCloud Service exposed by an ELB is reachable from anywhere unless marked Internal, then, is only reachable from within the VPC (or DuploCloud Infrastructure). Application ELBs allow you to use a certificate to terminate SSL on the LB and avoid providing application SSLs and certificates (e.g., [AWS Amazon Certificate Manager (ACM)](https://aws.amazon.com/certificate-manager/) certificates).

In Kubernetes, the platform creates a [NodePort ](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)pointing to the Deployment and adds the Worker Nodes' Host IPs to the ELB. Traffic flows from the client to the external port defined in the ELB (for example, 443), to the ELB's NodePort (for example, 30004 on the Worker Node), and the Kubernetes Proxy running on each Worker Node. The Worker Node forwards the NodePort to the container.&#x20;

#### **Classic ELB (Only applicable to Built-in container orchestration)**

Classic ELBs can be used when an application exposes non-HTTP ports that operate on any TCP port. Unless marked as Internal, Services exposed by an ELB are reachable from anywhere. Internal Services are reachable only from within the VPC (or DuploCloud infrastructure). Classic ELBs let you use a certificate to terminate SSL on the LB. This allows you to avoid providing application SSLs and certificates, such as [AWS Amazon Certificate Manager (ACM)](https://aws.amazon.com/certificate-manager/) certificates.

#### **Cluster IP (Kubernetes only)**

[Kubernetes ClusterIP](https://kubernetes.io/docs/concepts/services-networking/service/#type-clusterip) Load Balancers can be used if you are required to expose the application only within the Kubernetes Cluster.
