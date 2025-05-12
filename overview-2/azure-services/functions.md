---
description: Using Azure Function Apps in DuploCloud
---

# Function Apps

Azure Function Apps allow you to run serverless, event-driven code that automatically scales with demand. You can deploy Function Apps from the DuploCloud Portal using either built-in runtimes or Docker images.

## Creating a Function App Resource

1. In the DuploCloud Portal, navigate to **Cloud Services** → **Serverless**.
2. Select the **Function Apps** tab.
3.  Click **Add**. The **Add Function App** pane displays.\


    <figure><img src="../../.gitbook/assets/funtion complete.png" alt=""><figcaption></figcaption></figure>
4. Complete the fields:

<table data-header-hidden><thead><tr><th width="207.7777099609375"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for the Function App.</td></tr><tr><td><strong>Deploy from Package</strong></td><td>Select <strong>Yes</strong> to upload a deployment package (ZIP file) containing your function code. Select <strong>No</strong> to configure the app without a pre-built package.</td></tr><tr><td><strong>Storage Account</strong></td><td>Select an existing storage account. This is required for the Function App to manage state.</td></tr><tr><td><strong>Runtime Stack</strong></td><td>Choose the function runtime environment (e.g., <strong>Node.js</strong>, <strong>Python</strong>, <strong>.NET</strong>).</td></tr><tr><td><strong>Version</strong></td><td>Select the runtime version (e.g., <strong>3.1</strong>).</td></tr><tr><td><strong>Plan Type</strong></td><td>Choose the hosting plan (e.g., <strong>Consumption (Serverless</strong>), <strong>Premium</strong>, or <strong>App Service Plan</strong>).</td></tr><tr><td><strong>App Settings</strong></td><td>(Optional) Define key-value pairs for environment variables used by the function.</td></tr><tr><td><strong>Connection Strings</strong></td><td>(Optional) Specify database or service connection strings the function will use.</td></tr></tbody></table>

5. Click **Create**. The Function App URL is published in the DuploCloud portal. You can view the function app by opening the URL in the browser.
