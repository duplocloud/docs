# MCP Server

MCP (Model Context Protocol) servers extend the AI agent with external tool capabilities. Once an MCP server is registered in DuploCloud AI Suite, agents can call its tools from any ticket that includes the server's scope.

MCP servers are configured at the workspace level under **AI Admin → MCP Servers**. Two configuration methods are available: **HTTP/SSE** for standard remote MCP endpoints, and **Raw** for full control via a custom JSON config blob.

---

## Method 1: HTTP/SSE

### Step 1 — Add MCP Server

Navigate to **AI Admin → MCP Servers** and click **+ Add Server**. The **Add MCP Server** form opens. Fill in:

- **Name** — a display name for the server (e.g. `Linear`)
- **Description** — optional
- **Provider Type** — optional; links the server to a provider category for organizational purposes
- **Config Type** — select `HTTP/SSE`
- **API Endpoint** — the MCP server's HTTP endpoint URL (e.g. `https://mcp.linear.app/mcp`)
- **Transport** — `http` for standard HTTP or `sse` for Server-Sent Events

Click **Create**.

![](<../../.gitbook/assets/mcp-server-step-01.png>)

### Step 2 — Server Added

A success banner confirms the server was saved. The MCP Servers page shows the new server as a card with its endpoint URL. It is now available to be linked to any scope across all workspaces.

![](<../../.gitbook/assets/mcp-server-step-02.png>)

### Step 3 — Navigate to Providers

To make the MCP server accessible to an agent you need a **Provider** with credentials and a **Scope** that links both. Navigate to **AI Admin → Providers** and select the relevant category tab (e.g. **Other** for tools like Linear).

![](<../../.gitbook/assets/mcp-server-step-03.png>)

### Step 4 — Create Provider

Click **+ Add**. Fill in the **Add Provider** form:

- **Name** — a name for this provider (e.g. `Linear`)
- **Description** — optional
- **Type** — the provider category (e.g. `Other`)
- **Account ID** — an identifier for the provider account; can be any string if not required for routing

Click **Create Provider**.

![](<../../.gitbook/assets/mcp-server-step-04.png>)

### Step 5 — Provider Created

The provider detail page opens with the **Credentials** tab (empty) and **Scope** tab. The right panel confirms the category, type, and account ID.

![](<../../.gitbook/assets/mcp-server-step-05.png>)

### Step 6 — Add Credential

Click **+ Add** on the Credentials tab. The **Add Credential** modal opens. Fill in:

- **Name** — the credential set name (e.g. `Linear-credentials`)
- **Credential Fields** — one or more key/value pairs for the secrets this provider requires:
  - **Key** — the field name (e.g. `LINEAR_API_KEY`)
  - **Value** — the actual secret value
  - **Type** — `String` for most secrets
  - **Sensitive** — toggle on to store the value encrypted and mask it in the UI

Click **Create**.

![](<../../.gitbook/assets/mcp-server-step-06.png>)

### Step 7 — Add Scope

Click **+ Add** on the **Scope** tab. The **Add Scope** modal opens. Fill in:

- **Name** — the scope name used when creating tickets (e.g. `Linear-Test-MCP`)
- **Credential** — select the credential set created in the previous step
- **MCP Server** — select the MCP server to link (e.g. `Linear`)
- **Resource Map** — optional key/value pairs for additional context passed to the agent

Click **Create**.

![](<../../.gitbook/assets/mcp-server-step-07.png>)

### Step 8 — Agent Using the MCP Server

With the scope configured, create a ticket and select the scope (e.g. `Linear-Test-MCP`). The agent automatically has access to the Linear MCP tools. When prompted it calls the relevant tool — here `mcp__Linear__list_issues` — using the credentials bound to the scope.

![](<../../.gitbook/assets/mcp-server-step-08.png>)

### Step 9 — Agent Response

The agent returns structured data from the MCP tool. In this example it lists all 13 issues across the Linear workspace with their ID, title, status, priority, and team.

![](<../../.gitbook/assets/mcp-server-step-09.png>)

---

## Method 2: Raw JSON

The Raw config type gives full control over the MCP server configuration as a JSON blob. This method supports **credential placeholders** so secrets and per-environment values are resolved at runtime rather than being stored inline in the config. See [Credential Placeholders](credential-masking-for-mcp-servers.md) for the full reference.

### Step 1 — Add MCP Server with Raw Config

Navigate to **AI Admin → MCP Servers** and click **+ Add Server**. Fill in:

- **Name** — e.g. `Grafana`
- **Provider Type** — optional; select the relevant category (e.g. `OpenTelemetry`)
- **Config Type** — select `Raw`
- **Raw Config** — paste the full MCP server JSON. Use `${credential.<key>}` placeholders for any values that should be resolved from the scope's bound credentials at runtime.

For example:

```json
{
  "mcpServers": {
    "grafana": {
      "command": "uvx",
      "args": ["mcp-grafana"],
      "env": {
        "GRAFANA_URL": "${credential.url}",
        "GRAFANA_SERVICE_ACCOUNT_TOKEN": "${credential.token}"
      }
    }
  }
}
```

Click **Create**.

![](<../../.gitbook/assets/mcp-server-step-10.png>)

### Step 2 — Navigate to Providers

Navigate to **AI Admin → Providers** and select the category tab matching your server's provider type (e.g. **Observability** for Grafana).

![](<../../.gitbook/assets/mcp-server-step-11.png>)

### Step 3 — Create Provider

Click **+ Add**. Fill in the **Add Provider** form:

- **Name** — e.g. `Grafana`
- **Type** — e.g. `OpenTelemetry`
- **Account ID** — an identifier for the account (e.g. `grafana.com`)

Click **Next** to proceed directly to the Credentials step, or **Create** to save and configure credentials separately.

![](<../../.gitbook/assets/mcp-server-step-12.png>)

### Step 4 — Add Credentials

The **Credentials** step configures the secrets that will be injected into the Raw Config placeholders. Fill in:

- **Name** — the credential set name (e.g. `default`)
- **Credential Fields** — add one field per placeholder key used in the Raw Config. The field names must **exactly match** the placeholder keys — case-sensitive:
  - `token` → resolves `${credential.token}`
  - `url` → resolves `${credential.url}`

Mark sensitive fields (like tokens and passwords) as **Sensitive** to store them encrypted.

Click **Create** then **Next**.

![](<../../.gitbook/assets/mcp-server-step-13.png>)

### Step 5 — Create Scope

The **Scope** step links the credential set to the MCP server. Fill in:

- **Name** — e.g. `Grafana-MCP`
- **Credential** — pre-filled with the credential created in the previous step
- **MCP Server** — select the Raw MCP server (e.g. `Grafana`)
- **Resource Map** — optional

Click **Create**.

![](<../../.gitbook/assets/mcp-server-step-14.png>)

### Step 6 — Provider Ready

The Providers list now shows the Grafana provider alongside other observability providers.

![](<../../.gitbook/assets/mcp-server-step-15.png>)

### Step 7 — Agent Using the MCP Server

Create a ticket with the `Grafana-MCP` scope. Before the session starts, the platform resolves all `${credential.*}` placeholders in the Raw Config using the bound credentials, then writes the resolved `.mcp.json` for the agent. The agent calls Grafana MCP tools transparently.

![](<../../.gitbook/assets/mcp-server-step-16.png>)

### Step 8 — Agent Response

The agent returns live data from Grafana via the MCP tool. In this example it lists all 38 Grafana dashboards found in the workspace.

![](<../../.gitbook/assets/mcp-server-step-17.png>)
