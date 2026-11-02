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

Placeholders are resolved only in a raw config that defines exactly one server under `mcpServers`. A raw config with more than one server is skipped.

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

![Raw config with credential placeholders](<../../.gitbook/assets/credential-masking-step-01-raw-config.png>)

**Bound credential on the scope:**

The credential fields must match the placeholder keys exactly. For the config above, the credential must have a field named `token` and a field named `url`:

![Credential fields token and url](<../../.gitbook/assets/credential-masking-step-02-credential-fields.png>)

**Resolved `.mcp.json` written for the agent:**

```json
{
  "mcpServers": {
    "grafana": {
      "command": "uvx",
      "args": ["mcp-grafana"],
      "env": {
        "GRAFANA_URL": "https://grafana.example.com",
        "GRAFANA_SERVICE_ACCOUNT_TOKEN": "<resolved token value>"
      }
    }
  }
}
```

The raw config stored on the server is never modified and never contains the secrets. The resolved `.mcp.json`, which does contain them, is written fresh before every request to the agent, so a change to the credential or to the ticket's scopes takes effect on the next message.

---

## Naming Requirements

The key after `credential.` or `credential.metadata.` must **exactly match** the credential field name, including case. For example:

- `${credential.token}` requires a credential field named exactly `token`
- `${credential.url}` requires a credential field named exactly `url`
- `${credential.metadata.api-key}` requires a metadata key named exactly `api-key`

---

## Missing Keys Fail Loud

If any placeholder references a key that does not exist on the bound credential:

1. The **entire MCP server** is dropped from `.mcp.json` for that request
2. A `WARNING` is logged by the platform
3. The system prompt's **`## Connected MCP Servers`** section marks the server as `(FAILED TO LOAD)`, listing the missing key names and the credential name

This means the agent can see exactly what is missing and report it to the user — for example: *"The Grafana MCP server failed to load because the bound credential `default` is missing the key `token`."*
