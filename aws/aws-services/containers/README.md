---
description: Using containers and DuploCloud Services with AWS EKS and ECS
---

# Containers and Services

## DuploCloud Services and Containers <a href="#5-toc-title" id="5-toc-title"></a>

DuploCloud supports Elastic Kubernetes Service (EKS/ECS) out of the box. You can also deploy native Docker containers in virtual machines (VMs) with the DuploCloud platform.&#x20;

Adding a Service in the DuploCloud Platform is not the same as adding a Kubernetes service. When you deploy DuploCloud Services, the platform implicitly converts your DuploCloud Service into either a deployment set or a StatefulSet. The service is mapped to a deployment set if there are no volume mappings. Otherwise, it is mapped to a StatefulSet, which you can force creation of if needed. Most configuration values are self-explanatory, such as **Images**, **Replicas,** and **Environmental Variables**.

Kubernetes clusters are created during Infrastructure setup using the **Administrator -> Infrastructure** option in the DuploCloud Portal. The cluster is created in the same Virtual Private Cloud (VPC) as the Infrastructure. Building an Infrastructure with an EKS/ECS cluster may take some time.&#x20;

Next, you deploy an application within a Tenant in Kubernetes. The application contains a set of VMs, a Deployment set (Pods), and an application load balancer. Pods can be deployed either through the DuploCloud Portal or through `kubectl,`using HelmCharts.

{% hint style="info" %}
When you create a service, refer to the registry configuration in **DevOps** -> **Containers** -> **EKS/Native** **| ECS** -> **Services**, in the **Configuration** tab. Note the values in the **Environment Variables** and **Other Docker Config** fields.&#x20;

For example:&#x20;

`{"DOCKER_REGISTRY_CREDENTIALS_NAME":"registry1"}`
{% endhint %}
