---
description: Configure Okta for identity management in DuploCloud
---

# Okta Identity Management

[Okta](https://www.okta.com/intro-to-okta/) is a cloud-based identity and access management platform that provides secure Single Sign-On (SSO), multi-factor authentication (MFA), and lifecycle management for users across applications.&#x20;

DuploCloud supports using Okta as a source for user authentication and authorization. This integration allows you to log in to DuploCloud and manage user roles, permissions, and platform access using Okta. Okta's group-based permissions system can also be mapped to DuploCloud's user management to manage access to various services within DuploCloud.

This configuration requires some changes that require the DuploCloud support team to work together with you. Please reach out to your support team to get this setup.

## Managing Okta Users, Permissions, and API Tokens

Once the initial integration is setup and fully configured, you can use the [Okta Portal](https://login.okta.com/) to add users, assign roles and permissions, delete users, revoke permissions, and generate and manage Okta API tokens. See the Okta documentation for specific tasks:

* **Add and Manage Okta Users:**
  * [Add Okta users](https://help.okta.com/en-us/content/topics/users-groups-profiles/usgp-people.htm?cshid=ext_Directory_People)
  * [Manage users](https://help.okta.com/en-us/content/topics/users-groups-profiles/usgp-people.htm?cshid=ext_Directory_People)
* **Assign Roles and Permissions:**
  * [Manage administrative roles](https://help.okta.com/en-us/content/topics/security/administrators-set-up-admins.htm)
  * [Assign a role to a user](https://help.okta.com/wf/en-us/content/topics/workflows/connector-reference/azuread/actions/assignroletouser.htm)
* **Delete Users:**
  * [Delete a user](https://help.okta.com/oie/en-us/content/topics/users-groups-profiles/usgp-deactivate-user-account.htm)
* **Revoke Permissions:**
  * [Remove or change an admin role](https://help.okta.com/oie/en-us/content/topics/security/admin-remove-assignment.htm)
* **Generate and Manage Okta API Tokens:**
  * [Create an Okta API token](https://help.okta.com/en-us/content/topics/security/api.htm#create-okta-api-token)
  * [Manage Okta API tokens](https://help.okta.com/en-us/content/topics/security/api.htm)

