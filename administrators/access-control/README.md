# Access control

There are the following types of User roles in the DuploCloud system

* **Administrator**, has access to all tenants plus the administrative functions like plan configuration, system dashboard, system faults etc.
* **User**, regular users that can be given access to a specific tenant. A tenant could have multiple . users assigned.
* **Security,** meant for security and compliance auditors to check on security and compliance dashboards and reports.
* **Signup,** a specialized role meant for users creating and managing DuploCloud resources via API.

### Creating or Updating a User role

A new user is created by going to Administrator->Users and clicking on **+Add.** Similarly, an existing user can be updated using the same view.

&#x20;                                   ![](<../../.gitbook/assets/Screen Shot 2022-06-30 at 12.16.03 AM.png>)

### Single Sign On (SSO)

The user name is meant to be an email address associated with an Identity provider. Currently supported identity providers are Google and Microsoft Azure. Once a user is created in DuploCloud portal, the user receives an account-creation email with login instructions. No password are involved, the user simply has to navigate to their DuploCloud environment and use SSO to login to their account.

![](<../../.gitbook/assets/Screen Shot 2022-06-30 at 12.18.51 AM.png>)
