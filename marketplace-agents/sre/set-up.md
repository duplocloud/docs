---
description: What you need before you start, how to activate SRE from the Agent Marketplace, and how to create your first alert hub.
---

# Set Up

## Before you start

- **At least one observability scope** in your workspace (for example OpenTelemetry, Datadog, New Relic or Sentry). The hub form requires one: investigations start from metrics, logs and traces.
- **Optional scopes** for the other places the agent should look: a Kubernetes scope, a cloud scope (AWS, GCP, Azure or on-prem), and source control scopes (GitHub, GitLab or Bitbucket) for your infrastructure-as-code and application repositories.
- **An alert source** that can send webhooks, such as Prometheus Alertmanager or Grafana.
- **Permissions** for the people who will use it, and for the identity your alert source uses (see [Permissions and Safety](permissions-and-safety.md)).
- **Optional:** a Slack app and channel for notifications, and a runbook location (GitHub repository, Confluence space, Google Drive folder, Notion page or a web page).

{% hint style="info" %}
SRE acts with the access of the scopes you attach to the hub. Attach the least access that still lets the agent find root causes. Read-only credentials are a good start.
{% endhint %}

<!-- VERIFY: the repo does not list specific cloud IAM actions, Kubernetes roles or API scopes, because access comes from the scopes you choose. Confirm with the owner whether we recommend a ready-made read-only policy per scope type (for example an AWS read-only policy and a Kubernetes view role) and add it here if so. -->

### Slack (optional)

Notifications use a Slack bot, not an incoming webhook.

| Item | Value |
| --- | --- |
| Slack app | A Slack app with the `chat:write` **bot** token scope, installed to your Slack workspace and invited to the channel (or `chat:write.public` for public channels). |
| Provider type | `slack` |
| Credential fields | The bot token (starts with `xoxb-`) and the channel ID (starts with `C`). Field names do not matter; they are recognised by their shape. |
| Scope | A scope bound to that credential. You pick it as the hub's notification scope. |

<!-- VERIFY: the hub form's Notifications page still says "webhook URL" and "Incoming Webhooks", but the backend and the Slack setup guide in the repo use a bot token and channel ID through chat.postMessage. This draft follows the code. Confirm which is shipped before publishing. -->

## Activate SRE

1. Open the **Agent Marketplace** and find **SRE**.
2. Select **Activate** and confirm.
3. When it finishes, **SRE** appears in the **Observability** section of the menu.

<!-- VERIFY: marketplace steps, button names and card name ("SRE", "SRE Workbench" or "AI SRE") are not in the repo. The menu path Observability > SRE comes from the manifest. Screenshots SR-01 and SR-02. -->

## Grant access

Give the people who will use it the permissions in [Permissions and Safety](permissions-and-safety.md). Several actions (investigate, skip, run a recommended action, edit the root cause, create runbooks, manage rules, split) are granted separately. The "all" permission does not include them.

## Create your first alert hub

1. Open **Observability > SRE**. If you have no hub yet, select **Create your first alert hub**. Otherwise select **Manage alert hubs** and add one.
2. **Basics.** Enter a hub name (2 to 60 characters: lowercase letters, numbers and dashes) and choose where alerts come from. A description is optional.
3. **Investigations.** Pick the scopes the agent can use while investigating, grouped as Observability (required), Kubernetes, Cloud, Infrastructure as code and Application code. Choose what the agent may run without asking a person: **Read-only** (the default for a new hub), **Custom**, or **Full access**.
4. **Remediation.** Choose what a recommended fix may do. By default a fix uses the same scopes as investigations. You can give fixes their own scopes and their own command rules. New hubs start with Custom rules, where anything not on the allow list asks a person.
5. **Advanced options (optional).** **Skills** (notes about your system), **Runbooks** (where your runbooks live and how new ones are added) and **Notifications** (the Slack scope).
6. Select **Create**.

<!-- VERIFY: step names and button labels come from the frontend source (Basics, Investigations, Remediation, Skills, Runbooks, Notifications); confirm on the live form (screenshots SR-03 to SR-07). -->

## Connect your alert source

1. When the hub is ready, the page shows its **Webhook URL**. It can take a few seconds to appear.
2. In your alert source (for example Prometheus Alertmanager or Grafana), add that URL as a webhook receiver.
3. Select **Send a test alert** to run a first investigation end to end.

The identity your alert source uses to call the webhook needs only the **Ingest alerts into a hub** permission (`sreworkbench.ingest`). Do not give it anything else.

<!-- VERIFY: how an external alert source authenticates to the webhook (which token or credential type it sends) is not described in the repo. Confirm with the owner and document it here, and confirm that the source's identity really is a platform identity with the ingest permission. -->
<!-- VERIFY: the "Send a test alert" button runs a real investigation (agent run, LLM usage). Confirm it is acceptable to recommend it as a first step. -->

Next: [Use](use.md).
