# Concepts

{% hint style="info" %}
Following concepts don't apply to ECS because that has proprietary policy model that will be explained in the later section
{% endhint %}

While deploying Dockerized applications, here are a few concepts and terminologies to be aware of

* **Hosts**: These are virtual machines (EC2 Instances). In case of EKS deployments they are also called Worker nodes. By default apps within a tenant are pinned to VMs in the same Tenant. In case of EKS we have the ability to deploy Hosts in a separate tenant and apps in other tenants can leverage these hosts. This is called the shared host model.  \
  This is not applicable to ECS Fargate.
* **Service**: This is a DuploCloud terminology and is not to be confused with "Kubernetes Service". This represents a micro-service defined by a Name, DockerImage and number of replicas in additional to many other optional parameters. Behind the scenes, a DuploCloud Service maps 1:1 either a DeploymentSet or StatefulSet based on wether the microservice has stateful volumes or not. There are tons are optional configurations associated with a service which represents various ways a docker containers can be run. A few of these are
  * Environment variables
  * Host Network Mode
  * Volume mounts
  * Entrypoint or command overrides
  * Resource caps
  * Health Checks
* **Allocation Tags**: If a service needs to be pinned to run only a specific set of hosts this can be achieved by setting a string on both the hosts as well as the Service. Allocation Tag is a case-insensitive substring match i.e. Allocation Tag specified on a service should be a substring of the tag specified on the host. For example a Host maybe tagged as _HighCpu;HighMem_ and the service if tagged _highcpu_ can be allocated on this host. But if the service is tagged _highcpu;gpu_ then it won't be as it need a host that has _highcpu;gpu_ where
  * If a service does not have any tag set then it can placed on any host.

{% hint style="info" %}
If the host is tagged with a specific value and you have services with same tag even then the host is available for any service which has **no tags.** So if you want exclusive assignment of a host to a set of services only then the only way of achieving this is to make sure every service in the tenant is tagged with some value.
{% endhint %}

In case of Kubernetes deployments the concept of allocation tags is realized by mapping it to labels on nodes and then node selector on the _Deploymentset or Statefulset_

* **Host Networking:** By default Docker containers have their own network addresses. But at times it is desirable that these containers could reuse the same network interface as the VM itself. This is called Host Network Mode.
*   **Load balancer:** Every service if it needs to be reached from other services would need to be exposed via a LoadBalancer. Following types of LBs are supported:

    * **Application ELB**: When exposed via an ELB the service will be reachable from anywhere unless it is marked as Internal, in which case it will be reachable only from within the VPC (or infrastructure). This type of LB allows you to also use a certificate for terminating SSL on the LB which provides an advantage that one does not have to deal with SSL and certs from the application. This is a certificate issued from AWS ACM.\
      In case of Kubernetes behind the scenes the platform creates a NodePort pointing to the DeploymentSet and adds the Host IPs of worker nodes to the ELB. The flow of traffic is Client --> External Port in ELB (Say 443)  --> ELB to Node port (Say 30004 on the Worker Node) ---> K8S Proxy Running on each Worker Node Forwards Node Port to Container
    * Classic ELB (Only applicable to Built-In Container Orchestration):   When exposed via an ELB the service will be reachable from anywhere unless it is marked as Internal, in which case it will be reachable only from within the VPC (or infrastructure). This type of LB allows you to also use a certificate for terminating SSL on the LB which provides an advantage that one does not have to deal with SSL and certs from the application. This is a certificate issued from AWS ACM.&#x20;



    {% hint style="info" %}
    Classic ELB can be used when the application is exposing non HTTP ports and operating on any TCP port.
    {% endhint %}



    * Cluster IP (K8S Only): This can be used when we are required to expose the application only within the Kubernetes Cluster.

