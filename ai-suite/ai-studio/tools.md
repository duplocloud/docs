# Tools

In the DuploCloud AI Suite, a Tool is a modular component that enables the DuploCloud AI Agent to go beyond conversation and interact directly with your infrastructure. Each Tool accepts an input, executes custom logic, and returns a string output, which the agent can use to make decisions, continue a conversation, or trigger follow-up actions. By defining Tools, you control what the AI Agent is capable of, ensuring it operates only within the boundaries you explicitly set.

Tools are built as Python classes that inherit from the `BaseTool` class in [LangChain](https://www.langchain.com/), making them compatible with LangChain-based agents and easily callable by the DuploCloud AI Agent. When a user query is received, the agent determines whether a Tool is needed, selects the appropriate one, passes in the relevant input, and uses the output to guide its next steps. You can create tools for:

* Querying tenant or infrastructure configuration
* Fetching deployment statuses, logs, or metrics
* Integrating with systems like Slack, PagerDuty, or GitHub
* Running scripted operations (e.g., restarting containers)
* Retrieving usage or billing data for reporting and cost insights

## Uploading Tool Packages

Each Tool in the DuploCloud AI Suite relies on a Python package that contains the logic it will execute. Before creating a Tool, upload your package to DuploCloud.

1. Navigate to **AI Suite** → **Studio** → **Tools**, and select the **Packages** tab.
2.  Click **Add**. The **Upload Package** pane appears.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (500).png" alt="" width="421"><figcaption><p>The <strong>Upload Package</strong> pane</p></figcaption></figure></div>
3. In the **Tool Name** field, provide a name for the package.
4. Click **Choose File**, and select a valid `.zip` file that contains your tool code.
5. Click **Upload** to add the package.

Once uploaded, the package will appear in the list under the **Packages** tab. You can then reference this package when creating a Tool by specifying its name and providing an install script.

## Creating a Tool

Add a custom Tool to the DuploCloud AI Suite to enable the DuploCloud AI Agent to import and execute it during its reasoning process.

1. From the DuploCloud Portal, navigate to **AI Suite** → **Studio** → **Tools**, and select the **Tools** tab.
2.  Click the **Add** button. The **Add Tool Definition** pane displays.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (501).png" alt=""><figcaption><p>The <strong>Add Tool Definition</strong> pane</p></figcaption></figure></div>
3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="176.6666259765625"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the Tool.</td></tr><tr><td><strong>Package</strong></td><td>Select the Python package file to install (a <code>.zip</code> file with your Tool). To upload a new package, select <strong>Add Package</strong>. </td></tr><tr><td><strong>Install Script</strong></td><td>Specify the shell command to install the package (e.g., <code>pip install duplo-tool-package-main.zip</code>).</td></tr><tr><td><p><strong>Build Environment</strong> </p><p><strong>Variables</strong></p></td><td><p>Define one or more variables required to initialize the Tool during setup. Each entry includes a <strong>Key</strong>, <strong>Value</strong>, and optional <strong>Mandatory</strong> flag.<br></p><p>The <code>init_code</code> key should include:</p><ul><li>A Python import statement to bring your Tool class into scope.</li><li>An instantiation statement that creates an instance named <code>tool</code>.</li></ul><p><strong>Example</strong>:</p><p><strong>Key</strong>: <code>init_code</code></p><p><strong>Value</strong>: </p><pre data-full-width="false"><code>from duplo_custom_tool.kubectl_tool import ExecuteKubectlCommandTool

# Initialize the tool
tool = ExecuteKubectlCommandTool()
</code></pre></td></tr><tr><td><strong>Deployment Environment Variables</strong></td><td>Enter runtime environment variables required by the Tool (for example, namespace or region) as key/value pairs.</td></tr><tr><td><strong>MetaData</strong></td><td>Optional metadata such as creator name, tags, or description as key/value pairs.</td></tr></tbody></table>

4. Click **Submit** to create the Tool. Once the Tool is created, it can be selected when [creating Agents](agent.md#creating-an-agent).&#x20;

## Managing Tools

After creating a Tool, you can manage it at any time:

1. Navigate to **AI Suite** → **Studio** → **Tools**, and select the **Tools** tab.
2. Click on a Tool name in the **NAME** column to view its details.
3. Select from the tabs at the top (e.g., **MetaData**, **Build Env Vars**, **Deployment Env Vars**, **Packages**, **Details**) to view different Tool components.
   * The **Details** tab shows a full JSON representation of the Tool definition.
4. Use the **Actions** button to **Edit** or **Delete** the Tool.

<figure><img src="../../.gitbook/assets/Screenshot (502).png" alt=""><figcaption><p>The exec_k8s_tool Tool details page with the <strong>Details</strong> tab and <strong>Actions</strong> menu selected</p></figcaption></figure>

