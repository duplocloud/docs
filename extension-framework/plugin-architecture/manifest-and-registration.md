# Manifest and Registration

A plugin registers with the core by sending a manifest — a single JSON document that declares the plugin's identity, its menu entries, and the data schemas it needs. The core validates this document, provisions storage, and issues a plugin token. No other setup is required.

## The Manifest

```json
{
  "plugin_id": "acme-billing",
  "name": "Acme Billing",
  "version": "1.2.0",
  "base_url": "https://acme.example.com/plugin",

  "menu_items": [
    {
      "id": "invoices",
      "label": "Invoices",
      "view": { "method": "GET", "path": "/invoices" },
      "actions": [
        { "id": "create", "method": "POST",   "path": "/invoices" },
        { "id": "void",   "method": "DELETE", "path": "/invoices/:id" }
      ]
    }
  ],

  "data_schemas": [
    {
      "collection": "invoices",
      "schema": { "...JSON Schema..." },
      "indexes": [ { "fields": ["customer_id"] } ]
    }
  ]
}
```

### Field Definitions

| Field | Description |
|---|---|
| `plugin_id` | Unique identifier for the plugin. Used as the namespace prefix in the database (`plugin_data.acme-billing.*`) and in proxy routes (`/plugin-proxy/acme-billing/...`). Must be lowercase, hyphen-separated, and globally unique within the core. |
| `name` | Human-readable display name shown in the admin UI and menu system. |
| `version` | Semver string. The core uses this to detect updates and determine whether to apply schema changes automatically or trigger a migration. |
| `base_url` | Root URL of the plugin service. The core appends the manifest paths to this URL when proxying requests. Must be reachable from the core at registration time. |
| `menu_items` | Array of menu entries to inject into the UI shell. Each entry has an `id`, a `label`, a `view` (a `GET` route that returns an HTML fragment), and an optional `actions` array (mutation routes). |
| `data_schemas` | Array of collection definitions. Each specifies a `collection` name, a JSON Schema (used as a Mongo `$jsonSchema` validator), and an optional `indexes` array. |

## Registration Flow

When the core receives a manifest, it executes these steps in order:

1. Validates the manifest against the core's own meta-schema. Returns `400` with validation errors if the manifest is malformed.
2. Probes the plugin's `/health` endpoint to confirm the service is live. Registration fails if health check does not return `200`.
3. Persists the plugin record, menu items, and action mappings to the core's registry.
4. Provisions MongoDB collections under the `plugin_data.{plugin_id}.*` namespace for every collection declared in `data_schemas`.
5. Attaches each declared JSON Schema as a MongoDB `$jsonSchema` validator on the corresponding collection.
6. Builds the declared indexes on each collection.
7. Issues the plugin a long-lived plugin token scoped to its own namespace and returns it in the registration response.

The plugin must store the plugin token securely. It is the plugin's credential for all subsequent calls to the storage API.
