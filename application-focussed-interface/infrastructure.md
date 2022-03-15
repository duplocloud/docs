# Infrastructure

Each infrastructure is a unique VPC, in a region with a Kubernetes (or ECS cluster or both). Infrastructure can be created with 4 basic inputs: Name, VPC CIDR, Number of AZs, Region and option to enable or disable a K8S/ECS cluster. Behind the scenes, the system will automatically create the subnets, NAT gateway, routes and the cluster in the given region.

![Menu to create Infrastructure](<../.gitbook/assets/Screen Shot 2022-03-12 at 7.30.34 PM.png>)

{% hint style="info" %}
A common use for Infrastructure is having for instance 2 infrastructures, one for prod and one for non-prod. Another one is having an infrastructure in a different region either for DR or localized deployments for clients in that region.
{% endhint %}

****
