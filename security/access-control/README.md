---
description: Roles and access types across the DuploCloud Portal
---

# Isolation

Isolation of concerns and environments is the most basic principle in any infrastructure security implementation. The cloud providers allow many constructs to implement this isolation to varying degrees. As an example one can isolate two workloads in completely different "cloud accounts", or different "VPCs" within the same account or different "security groups" within the same VPC. Then there are other constructs like IAM (AWS Roles, Azure managed Identity, GCP service accounts) or Kubernetes namespace and so forth. A big challenge is how do we bring together dozens of these security constructs and map them to an application centric isolation model.   &#x20;

* An **Administrator** has access to all Tenants plus access to administrative functions like Plan configuration, system dashboards, system defaults, etc.
* A **User** is a regular user that can be given access to a specific Tenant. A Tenant can be accessed by multiple users and a user can be given access to multiple Tenants.
* The **Security** role is for security and compliance auditors, in order to verify security and compliance dashboards and reports.
* The **Signup** role is for users who create and manage DuploCloud resources via API.

### Single Sign On (SSO)

The user name is meant to be an email address associated with an Identity provider. Currently, supported identity providers are Google and Microsoft Azure. Once a user is created in the DuploCloud portal, the user receives an account-creation email with login instructions. No passwords are involved, the user simply has to navigate to their DuploCloud environment and use SSO to log in to their account.

![](<../../.gitbook/assets/Screen Shot 2022-06-30 at 12.18.51 AM.png>)
