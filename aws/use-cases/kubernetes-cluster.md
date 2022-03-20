# Kubernetes Cluster

{% hint style="info" %}
Here we are only talking about the setup of the EKS control plane. The actual worker nodes and rest of the workload setup will be described within the Tenant.
{% endhint %}

In DuploCloud platform a Kubernetes Cluster maps to an [Infrastructure](../aws-services/infrastructure.md) The cluster can be created by creating an infrastructure from Administrator --> Infrastructure --> ADD Button. An E2E infrastructure with a EKS cluster takes up to 20 minutes. See the Infrastructure section for details on other elements of the form

![](<../../.gitbook/assets/image (15).png>)

{% hint style="warning" %}
At this moment per infrastructure only one EKS or ECS cluster is supported. One can have both EKS as well as ECS cluster but only 1 or 0 of each.&#x20;
{% endhint %}

Once the Infrastructure is in ready state, you can go inside the Infrastructure to see the Kubernetes details, including the token and config for Kubectl.&#x20;

When you create Tenants under the Infrastructure a separate namespace is created within the Kubernetes Cluster by the name duploservices-\<TenantName>
