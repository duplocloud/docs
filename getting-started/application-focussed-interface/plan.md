# Plan

## DuploCloud Plans

Corresponding to each Infrastructure is the concept of a Plan. A Plan is a placeholder or a template for configurations. These configurations are consistently applied to all Tenants within the Plan (or Infrastructure). Examples of such configurations are:

* Certificates available to be attached to Load Balancers in Tenants of this Plan
* Machine images
* WAF web ACLs
* Common IAM policies and SG rules to be applied to all resources in Tenants within the Plan
* Unique or shared DNS domain name where applications provisioned in Tenants within the Plan can have a unique DNS name in this domain
* Resource Quota: The plan also has a resource quota that is enforced in each of the Tenants within that Plan
* DB Parameter Groups
* Several policies and feature flags are to be applied at the infrastructure level on Tenants within the Plan

The figure below shows a screenshot of the plan constructs:

![](<../../.gitbook/assets/Screen Shot 2022-03-12 at 8.12.26 PM.png>)



## DuploCloud Plans and DNS considerations

When creating DuploCloud Plans and DNS names, consider the following to prevent DNS issues:

* Plans in different portals will delete each other's DNS records, so each portal must use a distinct subdomain for its Plans.
* DuploCloud Plans in the same portal can share a DNS domain without deleting each other's records. Duplo-created DNS names will always include the Tenant name, which prevents collisions.
* The recommended practice for most portals is to set all Plans to the same DNS name, including the `default` Plan.
* Ideally, custom subdomains will be set in the Plans before turning on shell, monitoring, or logging. If the DNS is changed later, those services may need to be updated.
