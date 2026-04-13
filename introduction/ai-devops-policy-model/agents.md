# Duplo DevOps Agent

The DuploCloud platform ships with the Duplo DevOps Agent out of the box.  This is the Agent that carries out all the DevOps work inside the platform. The Agent integrates seamlessly with your existing infrastructure and can be deployed immediately to automate routine operations and troubleshooting workflows.

The Agent operates within the boundaries defined by Providers and Scopes. Providers store the credentials for your cloud accounts, Kubernetes clusters, observability tools, and other services. Scopes define exactly which resources within those Providers an Agent can access. When an Agent is assigned to a workspace, it inherits only the Scopes granted to that Workspace — ensuring precise, auditable access control.

The Agent is used both for ad hoc tasks in Tickets and as a part of Projects. Within a Project, the agent may play different roles based on attached skills — for example, helping the users create a spec and plan and then helping to execute those actions in the execution phase.&#x20;



## Adding a Custom Agent

Users can create their own agents and give them access to work within the DuploCloud platform.&#x20;



1. Navigate to **Agents** and click **Add Agent**.&#x20;

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

2. Provide a **Name**, **Description**, an endpoint where the agent can be accessed and an API path where messages will be sent to converse with the agent.&#x20;

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

3. Click **Create** to add your Agent.
