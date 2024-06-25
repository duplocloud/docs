# Okta user management

Okta is a cloud-based identity and access management (IAM) platform that enables you to manage user authentication, authorization, and user lifecycle management across various applications and services. It provides a centralized solution for identity management, securely connecting users to your applications and data regardless of the cloud provider or the technology stack being used.

## Configure Okta as a user source for the DuploCloud Portal

To configure Okta as a user source for the DuploCloud Portal, you will need to modify the `Auth.config` file with the appropriate keys and values. This configuration will enable Okta as the authentication provider and map Okta user groups to roles in the DuploCloud Portal.

### **Step 1. Add the keys to `Auth.config`**:

Open the `Auth.config` file in a text editor and add the following key-value pairs:

```xml
xmlCopy code<configuration>
  <appSettings>
    <add key="EnableOktaUserSource" value="true" />
    <add key="OktaAdminGroupId" value="admin-group-id" />
    <add key="OktaReadOnlyGroupId" value="read-only-group-id" />
    <add key="OktaSecurityGroupId" value="security-group-id" />
    <add key="OktaSignUpGroupId" value="sign-up-group-id" />
    <add key="OktaTenantGroupPrefix" value="duploservices-" />
    <add key="OktaToken" value="okta-token" />
    <add key="OktaDomain" value="https://dev-32616951.okta.com/" />
    <add key="OktaClientId" value="client_id" />
    <add key="OktaClientSecret" value="specifysecret" />
    <add key="ENABLEOKTALOGIN" value="true" />
  </appSettings>
</configuration>
```

**Explanation of Keys**:

* `EnableOktaUserSource`: Enables Okta as a user source.
* `OktaAdminGroupId`: Okta group ID for admin users.
* `OktaReadOnlyGroupId`: Okta group ID for read-only users.
* `OktaSecurityGroupId`: Okta group ID for security users.
* `OktaSignUpGroupId`: Okta group ID for sign-up users.
* `OktaTenantGroupPrefix`: Prefix for tenant groups in Okta.
* `OktaToken`: API token for Okta.
* `OktaDomain`: Okta domain URL.
* `OktaClientId`: Client ID from Okta.
* `OktaClientSecret`: Client secret from Okta.
* `ENABLEOKTALOGIN`: Enables Okta login functionality.

#### **Restart the Service**:

After modifying the `Auth.config` file, restart the relevant service for the changes to take effect. This step ensures that the application reads the updated configuration.

### **Step 2. Find the Group ID in the Okta Portal**:

To map Okta groups to roles in the DuploCloud Portal, you need the group IDs from Okta:

* **Login to the Okta Admin Portal**.
* Navigate to **Directory** -> **Groups** from the left-side menu.
* Select the group you want to get the ID for.
* The group ID is part of the URL in the browser when viewing the group details.

### **Step 3. Generate an API Okta Token**:

An API token is required for Okta to communicate with your application. Here’s how to create it:

* **Login to Okta Admin Portal**.
* Navigate to **Security** -> **API** from the left-side menu.
* Go to the **Tokens** tab.
* Click **Create Token** to generate a new API token.
*   Follow the instructions on [how to manage API Okta tokens](https://help.okta.com/en-us/content/topics/security/api.htm?cshid=ext-create-api-token#create-okta-api-token).

    The generated token should be used in the `OktaToken` key in the `Auth.config` file.

By adding these keys to your `Auth.config` file and restarting the service, you configure the DuploCloud Portal to use Okta as its user source. This integration maps Okta user groups to specific roles in the portal, allowing for streamlined user management and authentication.

If you encounter any issues or need further assistance with the configuration, you can refer to the Okta [documentation](https://help.okta.com/en-us/content/topics/security/api.htm?cshid=ext-create-api-token#create-okta-api-token) or reach out to Okta support for more detailed guidance.
