# Tickets

The AI HelpDesk provides a conversational interface for managing infrastructure tasks through AI-powered Tickets. Each Ticket connects you to an intelligent AI Agent who can reason through problems, suggest commands, and collaborate with you in real time via the Canvas workspace.

## Creating a Ticket

To begin a new interaction, users create a Ticket within the context of a specific Tenant, ensuring that all Agent actions and suggestions occur within the correct infrastructure scope. When creating a Ticket, the system requires selecting an [AI Agent](../ai-studio/agents.md) with the appropriate domain expertise, such as Kubernetes operations, observability, or deployment troubleshooting. A ticket can include input from multiple Agents. This allows for collaboration across different domains (for example, Kubernetes and Observability) within the same troubleshooting session.

To create a Ticket, complete the following steps:

1. Navigate to **AI Suite** -> **HelpDesk**.&#x20;
2. Select the appropriate **Agent** and **Instance**. Other Agents can be assigned to the Ticket later if new capabilities are needed, see [Managing Tickets](tickets.md#managing-tickets) below.
3. In the **Message to Agent** field, describe your task or problem, or choose one of the provided prompts (for details on customizing prompt suggestions, see the [Agent documentation](../ai-studio/agents.md#customizing-prompt-suggestions)).
4. Click **Submit** to send the message and initiate the Ticket. The Canvas displays, providing a dynamic workspace to begin interacting with the AI Agent.

<figure><img src="../../.gitbook/assets/image (479).png" alt=""><figcaption><p>Initiating a new ticket in HelpDesk</p></figcaption></figure>

{% hint style="info" %}
Tickets can also be created and managed in Slack via the [HelpDesk Slack integration](slack-integration.md).
{% endhint %}

## Collaborating in the Canvas

Each Ticket provides a Canvas, a dynamic, interactive workspace. The Canvas preserves the state of the interaction, ensuring continuity across multiple exchanges and allowing users to collaborate with the AI Agent as a knowledgeable partner.

In the Canvas you can:

* Send messages to the AI Agent
* View the agent’s reasoning and suggestions
* Track task progress over time

<figure><img src="../../.gitbook/assets/Screenshot (911).png" alt=""><figcaption><p>Canvas in the AI HelpDesk</p></figcaption></figure>

## Reviewing Suggested Commands

As the conversation evolves, the AI Agent may propose command-line instructions based on the context of the Ticket. These suggestions appear within the Canvas and are fully interactive. You can:

* **Approve** the command, queuing it for execution the next time a message is sent to the Agent.
* **Reject** the command, optionally providing feedback such as preferences or restrictions (e.g., “Avoid using describe commands”).
* **Ignore** the suggestion, leaving it unacknowledged.
* **Execute** the command immediately within the Terminal.

<figure><img src="../../.gitbook/assets/image (478).png" alt=""><figcaption><p>An AI command suggestion and user response options</p></figcaption></figure>

## Taking Action in the Terminal

Embedded in the Canvas is a shared Terminal that gives you secure, real-time command-line access to your environment, directly from the workspace. You can respond to AI Agent suggestions or run your own diagnostics and scripts, while the Agent, if granted access, can view the commands you’ve executed and suggest its own. This creates a collaborative space for you and the AI Agent to can work together.

To access the Terminal:

1. Click **Terminal** in the Canvas and select the desired scope:
   * **Admin Terminal**: select for full environment-level access.
   * **Tenant Terminal**: select to limit commands to a specific Tenant.
   * **Specific container**: select a container to open a shell directly inside a running application container.
2. Type commands manually to perform diagnostics, run scripts, or verify application behavior.
3. Optionally enable **Share Context With Agent** so the AI Agent can observe your Terminal activity and provide real time guidance and suggestions.

<figure><img src="../../.gitbook/assets/Screenshot (913).png" alt=""><figcaption><p>Shared Terminal, ready for command input</p></figcaption></figure>

All Terminal input and output are automatically saved to the Ticket history. Shared context allows the Agent to provide more accurate suggestions in future interactions while you maintain control over what is shared.

## Using Agent-Suggested Resources

As part of a Ticket interaction, the AI Agent may provide helpful supporting resources in the form of clickable links, URLs and files. These assets are tailored to the specific context of your request and are intended to accelerate troubleshooting or task completion.

* **Clickable links**: follow Agent-provided links to web resources like access guides, external articles, or other resources relevant to your request.
* **URLs**: Open URLs in a new tab to access dashboards, CI/CD pipeline, logs, and more without leaving the Canvas, enabling monitoring or review of deployment activity.
* **Temporary files**: Access scripts, manifests, configuration templates, or log snapshots stored in a secure Canvas directory. View and edit them directly in the embedded Terminal, with changes visible to the Agent; the directory is automatically deleted when the Ticket is resolved or closed.

## Managing Tickets

DuploCloud HelpDesk allows you to manage your Tickets efficiently. You can access past Tickets for reference, assign a different AI Agent to a Ticket for additional expertise, switch between open Tickets, update Ticket status, or delete Tickets.&#x20;

1. From the HelpDesk, select one of the following options:

<table data-header-hidden><thead><tr><th width="217.33331298828125"></th><th></th></tr></thead><tbody><tr><td><strong>Ticket</strong></td><td>Click to create a new Ticket. </td></tr><tr><td><strong>History</strong></td><td><p>Click <strong>History</strong> to view and access past Tickets:<br></p><ul><li><strong>Open Ticket</strong>: Click the Ticket name to open the Ticket and continue interacting with it.</li><li><strong>Update Status</strong>: Click the Ticket status and select <strong>Open</strong>, <strong>In Progress</strong>, or <strong>Closed</strong>.</li><li><strong>Delete Ticket</strong>: Click the menu (<img src="../../.gitbook/assets/menu icon (24).avif" alt="" data-size="line">) on the Ticket row and select <strong>Delete</strong>.</li></ul></td></tr><tr><td><strong>Ticket ID</strong></td><td>Open a different Ticket by selecting its Ticket ID.</td></tr><tr><td><strong>Title</strong></td><td>Open a different Ticket by selecting its Title.</td></tr><tr><td><strong>Agent</strong></td><td>Select a different Agent to assign to the currently opened Ticket. Once selected, you can use the Canvas to interact with the new Agent. </td></tr><tr><td><strong>Status</strong></td><td>Update the Ticket status (<strong>Open</strong>, <strong>In Progress</strong>, <strong>Closed</strong>).</td></tr></tbody></table>

