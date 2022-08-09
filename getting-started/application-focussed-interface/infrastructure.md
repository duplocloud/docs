# Infrastructure

Each infrastructure is a unique VPC, in a region with a Kubernetes (or ECS cluster or both). Infrastructure can be created with 4 basic inputs: Name, VPC CIDR, Number of AZs, Region and option to enable or disable a K8S/ECS cluster. Behind the scenes, the system will automatically create the subnets, NAT gateway, routes and the cluster in the given region.

![Infrastructure Creation Screen](<../../.gitbook/assets/image (1) (2).png>)

If the Infrastructure requirement is to configure in custom Private/Public Subnet CIDR, it can be achieved using  **Advanced Options.**

{% hint style="info" %}
A common use for Infrastructure is having for instance 2 infrastructures, one for prod and one for non-prod. Another one is having an infrastructure in a different region either for DR or localized deployments for clients in that region.
{% endhint %}

***
