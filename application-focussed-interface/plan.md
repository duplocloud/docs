# Plan

Corresponding to each infrastructure is the concept of a Plan. Plan is a place holder or a template for configurations. These configurations are consistently applied to all tenants within the plan (or Infrastructure). Example of such configurations are:&#x20;

* Certificates available to be attached to load balancers in tenants of this plan
* Machine images
* WAF web ACLs
* Common IAM policies and SG rules to be applied to all resources in tenants within the plan.
* Unique or shared DNS domain name where applications provisioned in tenants within the plan can have a unique DNS name in this domain.
* Resource Quota: Plan also has a resource quota that is enforced in each of the tenants within that plan &#x20;
* DB Parameter Groups
* Several policies and feature flags to be applied at the infrastructure level on Tenants within the plan.&#x20;

The figure below shows a screenshot of plan constructs:

![](<../.gitbook/assets/Screen Shot 2022-03-12 at 8.12.26 PM.png>)
