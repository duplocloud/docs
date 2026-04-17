# Connecting Datadog to DuploCloud

This guide walks through adding Datadog as a provider in DuploCloud, configuring credentials, creating a scope, and querying Datadog data through the AI agent.

---

## Step 1 — Navigate to the Observability Providers

Go to **AI Admin** → **Providers** → **IT**, then click the **Observability** tab. This lists all observability providers connected to your account.

![Observability providers list](../../.gitbook/assets/datadog-step-20.png)

---

## Step 2 — Add a New Provider

Click **+ Add**. Fill in the provider details:

- **Name** — a name to identify this provider
- **Type** — select the provider type (e.g. Trending)
- **Account ID** — a label to identify this account within DuploCloud

![Add Provider form](../../.gitbook/assets/datadog-step-22.png)

Click **Create Provider**.

---

## Step 3 — Add Credentials

The new provider opens on the **Credentials** tab. Click **+ Add** to add a credential. Fill in the credential fields:

- **api_key** — your Datadog API key
- **application_key** — your Datadog application key
- **url** — your Datadog site URL (e.g. `api.datadoghq.com`)

> **Where to find these values:** Both the API key and Application key must be created directly in Datadog under **Organization Settings → API Keys** and **Application Keys**. The site URL can be copied from your browser's address bar when logged into Datadog — use the base domain (e.g. `api.datadoghq.com` for US, `api.datadoghq.eu` for EU).

![New provider with Credentials tab](../../.gitbook/assets/datadog-step-24.png)

![Add Credential form](../../.gitbook/assets/datadog-step-13.png)

Enter your Datadog site URL in the **url** field.

![Entering the site URL](../../.gitbook/assets/datadog-step-14.png)

Toggle **Sensitive** on for fields containing secrets to ensure they are stored securely.

![Marking fields as sensitive](../../.gitbook/assets/datadog-step-15.png)

Click **Create** to save the credential.

---

## Step 4 — Add a Scope

Switch to the **Scope** tab and click **+ Add**. Fill in:

- **Name** — a label for this scope
- **Credential** — select the credential you just created
- **Description** — optional context for the agent

![Add Scope form](../../.gitbook/assets/datadog-step-02.png)

Click **Create**. The scope appears in the list.

![Scope created](../../.gitbook/assets/datadog-step-03.png)

---

## Step 5 — Use Datadog in a Ticket

Go to **AI DevOps** → **HelpDesk** → **Add Ticket**. Select **generic-agent** as the agent and choose your Datadog scope from the scope dropdown.

![Ticket with Datadog scope selected](../../.gitbook/assets/datadog-step-10.png)

Enter your request — for example, asking the agent to check alerts or synthetic monitors for a domain.

![Ticket prompt entered](../../.gitbook/assets/datadog-step-07.png)

Click **Create Ticket**.

---

## Step 6 — Agent Queries Datadog

The agent processes the request, connects to Datadog using the scope credentials, and returns the results.

![Agent processing the Datadog request](../../.gitbook/assets/datadog-step-11.png)

The response includes the relevant Datadog data — alert states, synthetic test results, monitor details, and a plain-language summary.

![Datadog results returned](../../.gitbook/assets/datadog-step-12.png)
