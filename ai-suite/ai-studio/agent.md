---
description: this page will be the technical of how to create an agent
---

# Agent

Agents are the core AI components in DuploCloud AI Suite. Each Agent is responsible for interpreting user inputs, deciding which Tools to invoke, and orchestrating intelligent responses using integrated data and logic. They serve as the execution layer for AI-powered workflows and can be tailored to a wide range of use cases, from conversational interfaces to backend automation.

DuploCloud supports two types of Agents: Prebuilt and Dynamic. Each offers a different development path, depending on whether you're deploying an existing containerized service or creating a prompt-driven AI workflow within DuploCloud.

## Step 1: Create an Agent

### Creating a Prebuilt Agent

Prebuilt Agents use a pre-existing container image that defines your Agent’s functionality. For specifics about Prebuilt Agents, see the [Developers documentation](developers.md).

1. Navigate to **AI Suite** → **Studio** → **Agents**.
2.  Click **Add**. The **Add Agent Definition** pane displays.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (504).png" alt="" width="563"><figcaption><p>The <strong>Add Agent Definition</strong> pane</p></figcaption></figure></div>
3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="220.22222900390625"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the Agent.</td></tr><tr><td><strong>Agent Type</strong></td><td>Select <strong>Prebuilt</strong>.</td></tr><tr><td><strong>Docker Image</strong></td><td>Enter the full image path (e.g., <code>registry/myagent:latest</code>).</td></tr><tr><td><strong>Base64 Docker Registry Credential (Optional)</strong></td><td>Enter credentials if needed.</td></tr><tr><td><strong>Port</strong></td><td>Enter the port exposed by the container.</td></tr><tr><td><strong>Protocol</strong></td><td>Select the network protocol your Agent uses for communication (e.g., <strong>http</strong>, <strong>https</strong>, or <strong>grpc</strong>). This determines how external services connect to the containerized Agent.</td></tr><tr><td><strong>Token Limit</strong></td><td>Set the token output limit.</td></tr><tr><td><strong>Environment Variables</strong></td><td>Define key-value pairs (mark as mandatory if needed).</td></tr><tr><td><strong>Meta Data</strong></td><td>Optional key-value configuration.</td></tr></tbody></table>

4.  Click **Submit** to create the Agent. You can view your Agents on the **Agents** tab. \


    <figure><img src="../../.gitbook/assets/Screenshot (509).png" alt=""><figcaption><p>The <strong>Agents</strong> tab with the <code>kubernetes-agent</code> Agent displayed</p></figcaption></figure>

Once the Agent has been successfully completed, complete steps 2 and 3 below to deploy and register the Agent so it can be used with [DuploCloud's AI ServiceDesk](../ai-servicedesk/).

### Creating a Dynamic Agent

Dynamic Agents are configured using flexible, user-defined parameters, including tools, prompt behavior, and optional custom build variables. First create an Agent definition, and then build an Agent image based on its configuration.

#### Creating an Agent Definition

1. Navigate to **AI Suite** → **Studio** → **Agents**.
2.  Click **Add**. The **Add Agent Definition** pane displays.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (510).png" alt="" width="503"><figcaption><p>The <strong>Add Agent Definition</strong> pane<br></p></figcaption></figure></div>



<div align="left"><figure><img src="../../.gitbook/assets/Screenshot (511).png" alt="" width="494"><figcaption><p>Expanded <strong>Knowledge Sources</strong> section of the <strong>Add Agent Definition</strong> pane</p></figcaption></figure></div>

3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="193.55548095703125"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the Agent.</td></tr><tr><td><strong>Agent Type</strong></td><td>Select <strong>Dynamic</strong>.</td></tr><tr><td><strong>Prompt</strong></td><td>Enter the initial instruction or context that guides the Agent’s behavior and responses.</td></tr><tr><td><strong>Tools</strong></td><td>Select one or more registered Tools for the Agent to use. For more about using Tools, see the <a href="tools.md">DuploCloud Tools documentation</a>. </td></tr><tr><td><strong>Provider</strong></td><td>Select the Large Language Model (LLM) that will power the Agent (e.g., <strong>bedrock</strong> or <strong>Other</strong>.</td></tr><tr><td><strong>Model</strong></td><td>Choose the specific version or configuration of the selected LLM to use for this Agent.</td></tr><tr><td><strong>Temperature</strong></td><td>Set the randomness of responses (e.g., <strong>0</strong> for deterministic behavior).</td></tr><tr><td><strong>Token Limit</strong></td><td>Set the maximum number of tokens for responses (e.g., <strong>1000</strong>).</td></tr><tr><td><strong>Knowledge Sources</strong></td><td><p>Optionally, click the plus icon (<img src="../../.gitbook/assets/Screenshot (507).png" alt="" data-size="line">) to connect the Agent to a knowledge source such as a vector database collection. This allows the Agent to retrieve and use information from previously uploaded documents stored in a vector database. Complete the fields:</p><ul><li><strong>Vector DB:</strong> Select a previously created vector database to connect as a knowledge source.</li><li><strong>Collections:</strong> Choose one or more document collections within the Vector DB relevant to the Agent (required if Vector DB is selected).</li><li><strong>Description:</strong> Enter a brief summary of the knowledge source’s purpose or contents (optional).</li><li><strong>Meta Data:</strong> Add key-value pairs to filter or target specific content in the knowledge source (optional).</li></ul></td></tr><tr><td><strong>Meta Data</strong></td><td>Add custom key-value metadata to the Agent.</td></tr></tbody></table>

4. Click **Submit**. Once the Agent creation is complete, continue below to package your configuration into a deployable container image.&#x20;

#### Building an Image

Now that the Agent is created, trigger a build packages your dynamic Agent’s configuration, including prompts, tool selections, and variables, into a deployable container image.&#x20;

1. Go to the **Builds** tab on the Agent’s details page.
2. Click **Trigger**. The **Trigger Build** pane displays.
3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="219.333251953125"></th><th></th></tr></thead><tbody><tr><td><strong>Builder Docker Image</strong></td><td>This field is prepopulated based on your Agent configurations.</td></tr><tr><td><strong>Timeout</strong></td><td>Set a timeout for the build job (e.g., <strong>0</strong> for unlimited).</td></tr><tr><td><strong>Tools</strong> </td><td>Select one or more registered tools for the Agent to use. See the <a href="tools.md">Tools documentation</a> for more details.</td></tr><tr><td><strong>Build Environment Variables</strong></td><td>Define environment variables to initialize tool behavior.<br><strong>Example:</strong><br><strong>Key</strong>: <code>init_code</code><br><strong>Value</strong>: <code>from duplo_custom_tool import ExecuteKubectlCommandTool; tool = ExecuteKubectlCommandTool(); print(isinstance(tool, BaseTool)); print(type(tool))</code></td></tr><tr><td>  <strong>Mandatory</strong></td><td>Check if the variable is required.</td></tr><tr><td><strong>Custom Build Variables</strong></td><td>(Optional) Add any custom key/value pairs for build-time configuration.</td></tr></tbody></table>

4. Click **Submit** to begin packaging your configured Agent into a runnable container image. After the build is complete, proceed with steps 2 and 3 below to deploy the image and register the Agent.

## Step 2: Deploy the Agent Image

Once an Agent image is created, it must be deployed. Deploying the Agent makes it available for use on your infrastructure.

1. Select the **Images** tab on the Agent page (**AI Suite** → **Studio** → **Agents** → select Agent name).
2.  Click the menu icon (<img src="../../.gitbook/assets/menu icon.avif" alt="" data-size="line">) next to the Agent image and select **Deploy**. The **Deploy Image** pane displays with name and image fields prepopulated.\


    <figure><img src="../../.gitbook/assets/Screenshot (506).png" alt=""><figcaption><p>The <strong>Agent</strong> page with the <strong>Deploy Image</strong> pane </p></figcaption></figure>
3. Choose a deployment method:
   * **Quick Deploy**: Automatically sets up everything needed to run your Agent: it creates a DC Service, deploys a pod that runs the Agent container, and exposes it through a load balancer listener using the port specified during Agent creation.
   * **Advanced**: Allows full control over deployment settings, including network, scaling, and service options.
4.  Proceed through the remaining steps to complete the deployment, following the prompts based on whether you selected **Quick Deploy** or **Advanced**. Monitor the deployment status on the **Deployments** tab. \


    <figure><img src="../../.gitbook/assets/Screenshot (508).png" alt=""><figcaption><p>The Agent <strong>Deployment</strong> tab showing the deployment with <strong>Running</strong> status</p></figcaption></figure>

## Step 3. Register the Agent

Once your Agent has been successfully deployed, it must be registered so that the DuploCloud AI Suite can route queries to it.

1. Select the **Register** tab on the Agent page (**AI Suite** → **Studio** → **Agents** → select the Agent name).
2.  Click **Register**. The **Register Agent** pane displays.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (512).png" alt="" width="496"><figcaption><p>The <strong>Register Agent</strong> pane </p></figcaption></figure></div>
3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="182.88885498046875"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Provide a name for this Agent registration.</td></tr><tr><td><strong>Instanceid</strong></td><td>Enter the ID of the deployed instance (created during deployment).</td></tr><tr><td><strong>Allowed Tenants</strong></td><td>Select the tenants where this Agent is allowed to operate.</td></tr><tr><td><strong>Endpoint</strong></td><td>The service endpoint for the deployed Agent (prepopulated).</td></tr><tr><td><strong>Path</strong></td><td>The endpoint path that handles requests. You can retrieve this from the Agent's registration info, if needed: On the Register tab, click the menu icon (<img src="../../.gitbook/assets/menu icon (1).avif" alt="" data-size="line">) next to the Instance and select Edit. Copy the path from the Path field.</td></tr><tr><td><strong>Headers</strong></td><td>Optional key/value pairs to pass custom headers during API calls.</td></tr></tbody></table>

3. Click **Submit** to register the Agent. This Agent can now be utilized by the DuploCloud Service Desk. To learn how to configure and use Service Desk, see the [Service Desk documentation](../ai-servicedesk/).&#x20;

