---
description: Adding multiple DuploCloud Portals to the Main DuploCloud Login Screen
---

# Multiple Portal Login Options

DuploCloud allows you to add multiple DuploCloud portal logins to your main sign-in screen. Each portal represents a separate DuploCloud environment or account. After logging in, users can switch between these portals from within the DuploCloud Platform.

## Adding a DuploCloud Portal Account

Follow these steps to add a new DuploCloud portal account that will appear as a selectable login option on the main DuploCloud sign-in screen.

1. In the DuploCloud portal, navigate to **Administrator** -> **System Settings**.
2. Select the **System Config** tab.
3.  In the **DuploCloud Accounts** area at the bottom of the screen, click **Add**. The **Add DuploCloud Account** pane displays.\


    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (528).png" alt=""><figcaption><p><strong>Add DuploCloud Account</strong> pane</p></figcaption></figure></div>
4.  Complete the required fields:

    <table data-header-hidden><thead><tr><th width="164.4444580078125"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the portal account (e.g., <code>Corporate Portal</code>).</td></tr><tr><td><strong>URL</strong></td><td>Enter the full login URL for the portal (e.g., <code>https://corp.duplocloud.net</code>).</td></tr><tr><td><strong>Description</strong></td><td>Optionally, add additional details about the portal.</td></tr></tbody></table>
5. Click **Create** to save the new portal account and add it to your DuploCloud login page.
6. Repeat this process for each additional portal you want to add.

## Resources

* [Management Portal Scope](../welcome-to-duplocloud/application-focussed-interface/management-portal-scope.md)**:** Learn how each DuploCloud portal defines the environment and resources users can access.
* [SSO Configuration](sso-configuration/): Set up Single Sign-On (SSO) options, like Okta or Google, for each login portal.
* [User Access to DuploCloud](add-edit-or-delete-a-user.md): Control which users have access to each portal and what Tenants they can view or manage.
* [API Tokens](api-tokens.md): Use permanent or temporary tokens to automate access for specific users or systems tied to a portal.
