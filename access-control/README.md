---
description: Tools for Administrators in the DuploCloud Portal
cover: ../.gitbook/assets/Linkedin-bannerV3 (1).png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# User Administration

## Access roles

The DuploCloud Portal contains the following access roles:&#x20;

* An **Administrator** has access to all Tenants plus access to administrative functions like Plan configuration, system dashboards, system defaults, etc.
* A **User** is a regular user that can be given access to a specific Tenant. A Tenant can be accessed by multiple users and a user can be given access to multiple Tenants.
* The **Security** role is for security and compliance auditors, in order to verify security and compliance dashboards and reports.
* The **Signup** role is for users who create and manage DuploCloud resources via API.

## Single Sign On (SSO)

The user name is meant to be an email address associated with an Identity provider. Currently, supported identity providers are Google and Microsoft Azure. Once a user is created in the DuploCloud portal, the user receives an account-creation email with login instructions. No passwords are involved, the user simply has to navigate to their DuploCloud environment and use SSO to log in to their account.

![](<../.gitbook/assets/Screen Shot 2022-06-30 at 12.18.51 AM.png>)
