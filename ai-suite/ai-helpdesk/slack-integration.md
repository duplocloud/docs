---
description: >-
  Integrate Slack with AI Helpdesk to access AI support from your Slack
  workspace
---

# Slack Integration

The DuploCloud AI HelpDesk Slack integration lets you get AI-powered support directly in your Slack workspace. You can create and manage Tickets, interact with AI Agents, and approve commands without leaving Slack. The integration works across all your DuploCloud Portals and maintains your existing shared Slack channel workflows. When needed, you can also open the full HelpDesk interface to perform advanced actions.

Here’s a quick look at how DuploCloud AI Agents work inside Slack.

{% embed url="https://drive.google.com/file/d/10Yqo1_7wuZXLZkMGD0-QM4eUpVwiv99D/view?usp=sharing" %}

## Using the AI HelpDesk Slack Integration

### **Configuring Agent Permissions**

Configuring permissions lets AI Agents assume specific user identities for proper access when handling your requests in Slack.

1. Navigate to **Administrator** ->**Tenants**.
2. Select the **Tenant** name from the **NAME** column.
3. Select the **Settings** tab.
4.  Click **Add**. The **Add Tenant Feature** pane appears.\


    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (995).png" alt=""><figcaption><p><strong>Add Tenant Feature</strong> pane</p></figcaption></figure></div>
5. In the **Select Feature** list, choose **Other**.
6. In the **Configuration** field, enter: `helpdesk-impersonatable-users`
7. In the adjacent **Value** field, enter the usernames of the users the Agent can impersonate, separated by semicolons, e.g., `user1;user2;user3`.
8. Click **Add** to apply the setting. The users appear in the **Permissions** list box when creating a Slack Ticket.

### Starting a Conversation

1. In your Slack channel, mention the Slack Bot using `@DuploCloud AI`. One of the following things will happen:
   * **If the thread is already linked to a HelpDesk Ticket:** The AI Agent joins the conversation. You can interact with it directly to request updates, ask questions, or continue troubleshooting in the Slack thread.
   * **If the thread is not yet linked to a ticket:** The Slack Bot will prompt you to create one. Click **Create Ticket**, and a panel prompting you to enter details about your request will appear.&#x20;

<div align="left"><figure><img src="../../.gitbook/assets/Create Ticket.png" alt="" width="563"><figcaption><p>The <strong>Create Ticket</strong> panel in the Slack-HelpDesk integration</p></figcaption></figure></div>

2. Enter the following information to configure your Ticket:

<table data-header-hidden><thead><tr><th width="170.5555419921875"></th><th></th></tr></thead><tbody><tr><td><strong>Portal</strong></td><td>Select the DuploCloud Portal where the Ticket should be created.</td></tr><tr><td><strong>Tenant</strong></td><td>Choose the Tenant within the selected Portal. Only Tenants you have access to will appear.</td></tr><tr><td><strong>Agent</strong></td><td>Pick the AI Agent to handle your request. Each Agent specializes in specific tasks (Kubernetes, deployments, etc.). For more information, see the <a href="../ai-studio/agents.md#customizing-prompt-suggestions">Agent documentation</a>.</td></tr><tr><td><strong>Default</strong> <strong>Permissions</strong></td><td>Select the user identity the Agent should assume. Only users added in Tenant Settings (<code>helpdesk-impersonatable-users</code>) will appear. See the detailed steps for <a href="slack-integration.md#configuring-agent-permissions">Configuring Agent Permissions</a>.</td></tr></tbody></table>

3. The Slack backend creates a Ticket in the selected Tenant and assigns it to the chosen AI Agent. You can now interact with the AI Agent directly in the Slack thread. For more information about Tickets, see the [Tickets page](tickets.md).

### Interacting with Tickets in Slack

Once your Ticket is created, you can manage the Ticket and interact with the AI Agents directly in Slack.

1. The AI Agent posts updates, responses, and command suggestions in the thread. Review each suggested command and choose **Approve**, **Reject**, or **Ignore**. For more information about interacting with Tickets, see the [Tickets documentation](tickets.md).
2. Click **Submit**. Approved commands are executed in your connected DuploCloud Portal, with results shown directly in the Slack thread.

<div align="left"><figure><img src="../../.gitbook/assets/Response options (2).png" alt="" width="563"><figcaption><p>A command suggestion and response options in the Slack-HelpDesk integration</p></figcaption></figure></div>

### **Updating Ticket Context**

Updating Ticket context lets you change the Portal, Tenant, Agent, or Default Permissions for your Ticket mid-conversation, without starting over. This ensures the AI Agent is always working with the correct environment and permissions.

1. From the Ticket Slack thread, click the **menu icon** (<img src="../../.gitbook/assets/Screenshot (991).png" alt="" data-size="line">) and select **Update Context**.
2.  Modify any of the following: **Portal**, **Tenant**, **Agent**, or **Permission**s.\


    <div align="left"><figure><img src="../../.gitbook/assets/Update Ticket screen.png" alt="" width="563"><figcaption></figcaption></figure></div>
3. When updating the **Portal** or **Tenant**, specify the **Share Thread Context** and add a **New Message**, if needed:
   * **New Message**: Optionally, add a note or instruction for the AI Agent.
   * **Share Thread Context**: Choose whether the AI should retain the existing thread conversation in the updated context:
     * **Yes - Share all the thread messages:** Transfers the entire conversation history to the AI in the updated Ticket context.
     * **No - Do not share thread messages:** Updates the ticket context without transferring the previous thread messages. No historical data is transferred.
4. Click **Update** to apply your changes.

{% hint style="warning" %}
**Security Consideration:** Historical context may contain sensitive data (API keys, credentials). Use discretion when transferring.
{% endhint %}

### Opening a Ticket in HelpDesk

Some operations may require direct Helpdesk access. Opening a ticket in the Helpdesk gives you access to the full interface in the correct portal, allowing you to perform advanced operations not available in Slack.

1.  In your Slack thread, click **Open AI HelpDesk**.\


    <div align="left"><figure><img src="../../.gitbook/assets/helpdesk (1).png" alt="" width="563"><figcaption><p><strong>Open</strong> <strong>AI HelpDesk</strong> button in Slack</p></figcaption></figure></div>
2. The Ticket opens in HelpDesk in the correct Portal, where you can view details, manage actions, and access additional HelpDesk features. For more information about using HelpDesk, see the [AI HelpDesk documentation](./).

<figure><img src="../../.gitbook/assets/Helpdesk open (2).png" alt=""><figcaption><p>DuploCloud AI HelpDesk for a Ticket generated in Slack</p></figcaption></figure>
