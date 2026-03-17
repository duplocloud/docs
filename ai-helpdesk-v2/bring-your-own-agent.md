# Bring Your Own Agent

While DuploCloud's built-in Agents cover a wide range of standard DevOps and cloud operations, you can register your own custom Agents to handle workflows specific to your organization — stitching together your own toolset, internal systems, and processes. For example, you could build an Agent that triages customer support tickets by connecting to Zendesk alongside your cloud infrastructure, or one that enforces custom compliance checks against your internal policy database.

## Registering a Custom Agent

You can host your Agent anywhere. To make it available in the AI Helpdesk and let the AI Engineer use it, you only need to provide:

* **Endpoint** — the URL where your Agent is reachable
* **Messaging protocol** — the format used to communicate with your Agent

Once registered, the Agent appears alongside the built-in Agents and can be assigned to an Engineer. The Engineer can then delegate specific tasks or tickets to your custom Agent, exactly as it would with any out-of-the-box Agent.

## What You Can Build

Custom Agents are well-suited for tasks that require deep integration with your organization's specific tools and workflows — things the built-in Agents are not designed to handle. Some examples:

* Triaging and routing support tickets via a helpdesk tool like Zendesk or Jira
* Running custom compliance or policy checks against internal systems
* Automating workflows across tools your team already uses
