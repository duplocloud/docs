---
description: >-
  Set up Single Sign-On for DuploCloud using Microsoft Entra ID (formerly Azure
  AD) as your identity provider
---

# Microsoft Entra ID SSO Configuration

You can integrate Microsoft Entra ID (formerly Azure Active Directory) with DuploCloud to enable Single Sign-On (SSO) for your users.

To configure SSO in DuploCloud, you will:

1. Register a new application in Microsoft Entra ID.
2. Create a client secret.
3. Assign API permissions.
4. Provide the configuration values to DuploCloud Support.

## Step 1. Register your application in the Microsoft Entra ID portal

1. Follow Microsoft’s instructions to [register your application with Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app) using the following specifications:&#x20;
   * Enter a name, such as `duplo-app1`.
   * For **Supported account types**, select **Accounts in any organizational directory (Any Microsoft Entra ID directory - Multitenant)**.
   * Under **Redirect URI**, select **Web** and enter:\
     `https://PORTAL_DNS_NAME/app/signin-microsoft`, replacing `PORTAL_DNS_NAME` with your DuploCloud portal domain (e.g., `duplo.cloud.mycompany.com`).
2. Copy the **Application (client) ID** and the **Tenant ID**. You will need to provide these to DuploCloud Support in a future step.

## Step 2. Create a client secret for your application

1. Follow Microsoft’s instructions to [create a client secret for your application](https://learn.microsoft.com/en-us/entra/identity-platform/how-to-add-credentials?tabs=client-secret).
2. Copy and save the secret value immediately after creation, as Microsoft only shows it once.&#x20;

## Step 3. Assign API permissions

1. Follow Microsoft’s instructions in the [Add permissions to access Microsoft Graph](https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-configure-app-access-web-apis#add-permissions-to-access-microsoft-graph) section. When configuring permissions, be sure to:
   * Select **Microsoft Graph** and choose **Delegated permissions**.
   * Add the following delegated permissions (if not already present):
     * `openid`
     * `email`
     * `profile`
     * `User.Read`
   * Click **Add permissions**.
   * Click **Grant admin consent for Default Directory**, and confirm by clicking **Yes**.

These permissions allow DuploCloud to authenticate users and retrieve basic identity information during single sign-on. Granting admin consent ensures these permissions apply to all users in your organization.

## Step 4. Provide your application details to DuploCloud Support

Provide the following information to DuploCloud Support:

* Application (client) ID
* Client secret value
* Tenant ID

DuploCloud Support will complete the configuration of Microsoft Entra ID as your SSO provider.
