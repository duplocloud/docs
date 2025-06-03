# Ticket

The AI HelpDesk provides a conversational interface for managing infrastructure tasks through AI-powered tickets. Each ticket connects you to an intelligent AI Agent who can reason through problems, suggest commands, and collaborate with you in real time via the Canvas workspace.

## Creating a Ticket

To begin a new interaction, users create a ticket within the context of a specific Tenant. This ensures that all agent actions and suggestions occur within the correct infrastructure scope. Upon ticket creation, the system requires two key assignments: A designated human user responsible for communicating with the AI agent and overseeing the task, and an [AI agent](../ai-studio/agent.md), chosen for its domain expertise, such as Kubernetes operations, observability, or deployment troubleshooting.

**To create a ticket**:

1. Navigate to **AI Suite -> HelpDesk** pane.&#x20;
2. Selects the appropriate **Agent** and **Instance**.
3. Begin the interaction by submitting a **Message to Agent** to describe the task or problem.

## Collaborating in the Canvas

Each ticket includes a Canvas, which serves as a dynamic and interactive workspace for collaboration. The Canvas preserves the state of the interaction and ensures continuity across multiple exchanges. It allows you to interact with the AI agent acting as a knowledgeable partner.

In the Canvas you can:

* **Send messages** to the AI agent
* **View the agent’s reasoning** and suggestions
* **Track task progress** over time

## Receiving and Reviewing Suggested Commands

As the conversation evolves, the AI agent may propose command-line instructions based on the context of the ticket. These suggestions appear within the Canvas and are fully interactive. You can:

* **Approve** the command, queuing it for execution the next time a message is sent to the agent.
* **Reject** the command, optionally providing feedback such as preferences or restrictions (e.g., “Avoid using describe commands”).
* **Ignore** the suggestion, leaving it unacknowledged.
* **Execute** the command immediately within the Terminal.

## Taking Action in the Terminal

Embedded in the Canvas is a shared terminal that gives you secure, real-time command-line access to your environment, directly from the workspace. You can respond to agent suggestions or run your own diagnostics and scripts, while the agent, if granted access, can view the commands you’ve executed and suggest its own. This creates a collaborative space where both human and AI can work together efficiently.

All input and output in the terminal is automatically saved to the ticket history. If the "Share Context With Agent" checkbox is enabled, this activity is also shared with the agent the next time you send a message, enabling more accurate and informed responses while letting you control what context is available.

You can also launch shell sessions inside running application containers. During these sessions, the agent remains present and context-aware, offering assistance that’s tailored to the container’s environment. This makes it easier to debug, verify behavior, and resolve issues in place.

The shared terminal is central to how you and the agent collaborate, providing transparency, continuity, and the ability to act with confidence throughout the lifecycle of a ticket.

## Agent-Suggested Resources

As part of a ticket interaction, the AI agent may provide helpful supporting resources in the form of **URLs** and **files**. These assets are tailored to the specific context of your request and are intended to accelerate troubleshooting or task completion.

### **URLs**

In it's responses, the agent may include clickable URLs that point to relevant resources such as:

* Monitoring dashboards (e.g., Grafana, CloudWatch, Azure Monitor)
* CI/CD pipelines or deployment logs
* Relevant external documentation

You can click these links to open them in a new browser tab to access the data or tools while continuing your work in the Canvas.

### **Files**

When tasks require files, the agent can create a temporary directory within the ticket’s Canvas. This secure workspace may include:

* Shell scripts for automated fixes or deployments
* YAML files, configuration templates, or Kubernetes manifests
* Log snapshots or text artifacts

You can view and edit these files directly in the embedded Terminal. All changes are visible to the agent, allowing it to reason about or modify file contents in real time. Once the task is resolved or the ticket is closed, the system automatically deletes the directory to preserve cleanliness and security.

