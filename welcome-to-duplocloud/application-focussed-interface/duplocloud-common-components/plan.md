---
description: A conceptual overview of DuploCloud Plans
---

# Plan

## DuploCloud Plans

When you create an[ Infrastructure](infrastructure.md) in DuploCloud, a Plan is automatically generated. A Plan is a placeholder or a template for configurations. These configurations are consistently applied to all Tenants within the Plan (or Infrastructure). Examples of such configurations are:

* Certificates available to be attached to Load Balancers in the Plan's Tenants
* Machine images
* WAF web ACLs
* Common IAM policies and SG rules to be applied to all resources in the Plan's Tenants
* Unique or shared DNS domain names where applications provisioned in the Plan's Tenants can have a unique DNS name in the domain
* Resource Quota that is enforced in each of the Plan's Tenants
* DB Parameter Groups
* Policies and feature flags applied at the Infrastructure level on the Plan's Tenants

The figure below shows a screenshot of the plan constructs:

<figure><img src="../../../.gitbook/assets/Screenshot (245).png" alt=""><figcaption><p>The <strong>Capabilities</strong> tab for the <strong>NONPROD</strong> Plan in the DuploCloud Portal</p></figcaption></figure>

## DuploCloud Plans and DNS Considerations

When creating DuploCloud Plans and DNS names, consider the following to prevent DNS issues:

* Plans in different portals will delete each other's DNS records, so each portal must use a distinct subdomain for its Plans.
* DuploCloud Plans in the same portal can share a DNS domain without deleting each other's records. Duplo-created DNS names will always include the Tenant name, which prevents collisions.
* The recommended practice for most portals is to set all Plans to the same DNS name, including the `default` Plan.
* Ideally, custom subdomains will be set in the Plans before turning on shell, monitoring, or logging. If the DNS is changed later, those services may need to be updated.
