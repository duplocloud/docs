---
description: Provisioning Azure App Service Plans from the DuploCloud Portal
---

# App Service Plans and Web Apps

Azure App Services provide a way to host web applications in a fully managed platform-as-a-service (PaaS) environment. In DuploCloud, you can provision both App Service Plans and Web Apps directly from the UI.&#x20;

You must create an App Service Plan before you can deploy a Web App.

## Creating an App Service Plan

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Serverless**.
2. Select the **App Service Plan** tab.
3.  Click **Add**. The **Add App Service Plan** pane displays. \


    <div align="left"><img src="../../../../.gitbook/assets/image (129).png" alt="The Add App Service Plan pane" width="363"></div>
4. Complete the fields:&#x20;

<table data-header-hidden><thead><tr><th width="165.1112060546875"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Specify a unique name for the App Service Plan. </td></tr><tr><td><strong>Region / ASE</strong></td><td>Select the Azure Region where the Service Plan should exist.</td></tr><tr><td><strong>Platform</strong></td><td>Select the O/S type for the App Services to be hosted in this plan. Supported values include <code>Windows</code> and <code>Linux</code>.</td></tr><tr><td><strong>Server Size</strong></td><td>Select the SKU size for the plan.</td></tr><tr><td> <strong>No of Instances</strong></td><td>Specify the number of Workers (instances) to be allocated.</td></tr></tbody></table>

5. Click **Submit** to create the App Service Plan.&#x20;

## Creating a Web App Resource

After creating an App Service Plan, you can deploy a Web App resource that uses it. DuploCloud supports two deployment methods:

* **Code**: Choose a built-in runtime such as Node.js, Python, or .NET.
* **Docker**: Provide a container image to run in the Web App.

Complete the following steps to create a Web App Resource:

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Serverless**.
2. Select the **Web Apps** tab.
3. Click **Add**. The **Add Web App** pane displays.&#x20;

<div align="left"><img src="../../../../.gitbook/assets/image (129).png" alt="The Add App Service Plan pane" width="363"></div>

4. Complete the fields:&#x20;

<table data-header-hidden><thead><tr><th width="169.55548095703125"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for the Web App.</td></tr><tr><td><strong>App Service Plan</strong></td><td>Select the existing App Service Plan that will host this Web App.</td></tr><tr><td><strong>Publish</strong></td><td>Choose <strong>Code</strong> to use a built-in platform (e.g., Node.js, Python, or .NET). You can select from a list of available runtimes based on the platform you choose.<br>Choose <strong>Docker</strong> to deploy a container image. Provide a valid Docker image URL (e.g., <code>myregistry.azurecr.io/myapp:latest</code>) from a trusted container registry. Ensure the image exposes the correct port (usually <code>80</code>) and is accessible from Azure.</td></tr><tr><td><strong>Environmental Variables</strong></td><td>Enter key-value pairs to be passed into the application at runtime. Useful for configuration and secrets.</td></tr><tr><td><strong>Health Check Path</strong></td><td>The URL path (e.g., <code>/health</code>) used to check if the app is healthy. Azure uses this for app monitoring and scaling.</td></tr></tbody></table>

6. Click **Submit** to create the Web App Resource.&#x20;

<figure><img src="../../../../.gitbook/assets/image (468).png" alt=""><figcaption><p>The <strong>Web Apps</strong> tab in the DuploCloud Portal</p></figcaption></figure>
