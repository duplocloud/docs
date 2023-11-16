---
description: Using containers and DuploCloud Services with AWS EKS and ECS
---

# Containers and Services

## EKS/ECS support for containers and services <a href="#1-toc-title" id="1-toc-title"></a>

DuploCloud supports Elastic Kubernetes Service (EKS/ECS) out of the box.&#x20;

Kubernetes clusters are created during Infrastructure setup using the **Administrator -> Infrastructure** option in the DuploCloud Portal. The cluster is created in the same Virtual Private Cloud (VPC) as the Infrastructure. Building an Infrastructure with an EKS/ECS cluster may take some time.&#x20;

Next, you deploy an application within a Tenant in Kubernetes. The application contains a set of VMs, a Deployment set (Pods), and an application load balancer. Pods can be deployed either through the DuploCloud Portal or through `kubectl,`using HelmCharts.

## DuploCloud Services and Containers <a href="#5-toc-title" id="5-toc-title"></a>

You can deploy native Docker containers in virtual machines (VMs) with the DuploCloud platform. Adding a Service in the DuploCloud Platform is not the same as adding a Kubernetes service.&#x20;

Deploying DuploCloud Services implicitly converts Services into either a deployment set or a StatefulSet. If there are no volume mappings, then the service is mapped to a deployment set. Otherwise, it is mapped to a StatefulSet, which you can force creations of if needed. Most configuration values are self-explanatory, such as **Images**, **Replicas,** and **Environmental Variables**.

## Displaying Services <a href="#7-toc-title" id="7-toc-title"></a>

Once the deployment commands run successfully, click the **Services** tile on the **Tenants** page. Your deployments are displayed and you can now attach [load balancers](../load-balancers/) for the Services.

<div align="left">

<figure><img src="../../../.gitbook/assets/Services_display.png" alt=""><figcaption><p><strong>Tenants</strong> page with <strong>Services</strong> tile</p></figcaption></figure>

</div>

### Starting, stopping, and restarting multiple DuploCloud Services <a href="#7-toc-title" id="7-toc-title"></a>

Using the Services page, you can start, stop, and restart multiple services at one time.

1. In the DuploCloud Portal, navigate to **DevOps** -> **Containers** and select either **EKS/Native** or **ECS**.&#x20;
2. Click the **Services** tab.&#x20;
3. Use the checkbox column to select multiple services that you want to start or stop at once.
4. From the **Service Actions** menu, select **Start Service**, **Stop Service**, or **Restart Service.**

Your selected services are started, stopped, or restarted as you specified.

<div align="left">

<figure><img src="../../../.gitbook/assets/multiple_start_stop.png" alt=""><figcaption><p><strong>Services</strong> page with checkbox column (highlighted) and <strong>Service Actions</strong> menu</p></figcaption></figure>

</div>



{% hint style="info" %}
When you create a service, refer to the registry configuration in **DevOps** -> **Containers** -> **EKS/Native** **| ECS** -> **Services**, in the **Configuration** tab. Note the values in the **Environment Variables** and **Other Docker Config** fields.&#x20;

For example:&#x20;

`{"DOCKER_REGISTRY_CREDENTIALS_NAME":"registry1"}`
{% endhint %}

## Managing Docker, Kubernetes, and AWS configs and Secrets <a href="#6-toc-title" id="6-toc-title"></a>

See the [Configs and Secrets](../../use-cases/passing-secrets/) section for information about creating and managing:

* Docker Registry Credentials
* Configuration and secrets in AWS
* Passing Kubernetes ConfigMaps as Environment Variables (EVs) and files.
