# Duplo DevOps Agent

The DuploCloud platform ships with the Duplo DevOps Agent out of the box.  This is the Agent that carries out all the DevOps work inside the platform. The Agent integrates seamlessly with your existing infrastructure and can be deployed immediately to automate routine operations and troubleshooting workflows.

The Agent operates within the boundaries defined by Providers and Scopes. Providers store the credentials for your cloud accounts, Kubernetes clusters, observability tools, and other services. Scopes define exactly which resources within those Providers an Agent can access. When an Agent is assigned to a workspace, it inherits only the Scopes granted to that Workspace — ensuring precise, auditable access control.

The Agent is used both for ad hoc tasks in Tickets and as a part of Projects. Within a Project, the agent may play different roles based on attached skills — for example, helping the users create a spec and plan and then helping to execute those actions in the execution phase.&#x20;



## Adding a Custom Agent

Users can create their own agents and give them access to work within the DuploCloud platform.&#x20;



1. Navigate to **Agents** and click **+ Add**.&#x20;

![](<../../../.gitbook/assets/agents-step-01.png>)

2. Provide a **Name**, **Description**, an endpoint where the agent can be accessed and an API path where messages will be sent to converse with the agent.&#x20;

3. Optionally, expand the **Metadata** section to configure **prompt suggestions** and **prompt templates**. These help users get started quickly when creating a ticket — suggestions appear as one-click chips and templates pre-fill the input with parameterised content.

```yaml
STREAMING_ENABLED: 'true'
prompt_suggestions: '["Prompt 1", "Prompt 2", "Prompt 3"]'
prompt_templates: '[{"name":"Template Name","description":"Template description","content":"Template content with {{variable1}}, {{variable2}}, and {{variable3}}"}]'
```

- **`prompt_suggestions`** — a JSON array of short prompt strings shown as clickable chips on the ticket creation screen under **"Try one of these to get started"**
- **`prompt_templates`** — a JSON array of objects, each with a `name`, `description`, and `content`. The `content` supports `{{variable}}` placeholders that are filled in by the user. Templates appear under **"Or try a template"**

{% hint style="warning" %}
The values for `prompt_suggestions` and `prompt_templates` must be valid JSON encoded as a YAML string — wrap each value in single quotes. Do **not** nest single quotes inside the value. Use double quotes for all JSON keys and strings inside the array.
{% endhint %}

![](<../../../.gitbook/assets/agents-step-02.png>)

4. Click **Create** to add your Agent.

## Prompt Suggestions and Templates on the Ticket Screen

When a user creates a new ticket and selects this agent, the prompt suggestions appear as clickable chips below the input box under **"Try one of these to get started"**. The prompt templates appear below that under **"Or try a template"**.

![](<../../../.gitbook/assets/agents-step-03.png>)

Clicking any suggestion chip instantly populates the ticket input with that text. The user can edit it before submitting or click **Create Ticket** directly.

![](<../../../.gitbook/assets/agents-step-04.png>)

Each suggestion replaces whatever is currently in the input field. Clicking a new suggestion replaces the previous one — only one suggestion is active at a time.

![](<../../../.gitbook/assets/agents-step-05.png>)

Clicking a template pre-fills the input with the full template content including its `{{variable}}` placeholders. The user fills in the values before submitting.

![](<../../../.gitbook/assets/agents-step-06.png>)
