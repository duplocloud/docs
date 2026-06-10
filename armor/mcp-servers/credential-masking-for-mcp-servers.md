# MCP Credential Placeholders

Raw MCP server configs support credential placeholders — named variables that are resolved from the scope's bound credential immediately before the `.mcp.json` session file is written. This keeps secrets and per-environment values out of the server config entirely.

---

## Placeholder Syntax

Two forms are supported:

| Placeholder | Resolves from |
|---|---|
| `${credential.<key>}` | `Credential.Data["<key>"]` |
| `${credential.metadata.<key>}` | `Credential.MetaData["<key>"]` |

Lookups are **flat, case-sensitive, and exact-match**. Placeholders can appear anywhere inside a string value in the raw config tree — in `url`, `command`, items in `args`, values in `env`, `headers`, or any other string field. Multiple placeholders in a single string are supported.

---

## Example

**Raw config registered on the MCP server:**

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

![](<../../.gitbook/assets/mcp-server-step-10.png>)

**Bound credential on the scope:**

The credential fields must match the placeholder keys exactly. For the config above, the credential must have a field named `token` and a field named `url`:

![](<../../.gitbook/assets/mcp-server-step-13.png>)

**Resolved `.mcp.json` written for the session:**

```json
{
  "mcpServers": {
    "grafana": {
      "command": "uvx",
      "args": ["mcp-grafana"],
      "env": {
        "GRAFANA_URL": "https://system-svc-grafana-oc-default.ai-sandbox-apps.duplocloud.net",
        "GRAFANA_SERVICE_ACCOUNT_TOKEN": "<resolved token value>"
      }
    }
  }
}
```

The raw config stored on the server is never modified. Placeholder resolution happens in memory at session start and the resolved values exist only for the duration of that agent session.

---

## Naming Requirements

The key after `credential.` or `credential.metadata.` must **exactly match** the credential field name, including case. For example:

- `${credential.token}` requires a credential field named exactly `token`
- `${credential.url}` requires a credential field named exactly `url`
- `${credential.metadata.api-key}` requires a metadata key named exactly `api-key`

---

## Missing Keys Fail Loud

If any placeholder references a key that does not exist on the bound credential:

1. The **entire MCP server** is dropped from `.mcp.json` for that session
2. A `WARNING` is logged by the platform
3. The system prompt's **`## Connected MCP Servers`** section marks the server as `(FAILED TO LOAD)`, listing the missing key names and the credential name

This means the agent can see exactly what is missing and report it to the user — for example: *"The Grafana MCP server failed to load because the bound credential `default` is missing the key `token`."*
