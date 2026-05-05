# Storage API

All plugin persistence goes through a single generic storage API exposed by the core. Plugins never construct database connections or manage credentials — they make HTTP calls to one endpoint set, authenticated with their plugin token.

## Namespace Convention

Every plugin gets its own logical region of the database:

```
plugin_data.{plugin_id}.{collection}
```

For example, the `acme-billing` plugin with collections `invoices` and `customers` maps to:

```
plugin_data.acme-billing.invoices
plugin_data.acme-billing.customers
```

The namespace has four properties:

- **Isolation** — the plugin token is scoped to the plugin's prefix. A plugin cannot read or write outside its own namespace, even if it constructs a request targeting another plugin's collection name.
- **Discoverability** — all data a plugin owns can be listed with one prefix query. This makes uninstall and export operations straightforward — no cross-collection scanning required.
- **Schema independence** — two plugins can both declare a `customers` collection without collision. The full namespace path is always `plugin_data.{plugin_id}.customers`.
- **Migration scoping** — when a plugin updates its schema, migrations only touch its own collections. Other plugins are unaffected.

### Multi-Tenant Extension

In a multi-tenant deployment, extend the namespace with the tenant identifier:

```
plugin_data.{tenant_id}.{plugin_id}.{collection}
```

The token scoping and isolation guarantees apply at this extended path.

## Endpoints

```
POST   /api/storage/{collection}           create document
GET    /api/storage/{collection}           query (with filters as query parameters)
GET    /api/storage/{collection}/{id}      read one document by ID
PATCH  /api/storage/{collection}/{id}      partial update
DELETE /api/storage/{collection}/{id}      delete document
```

`{collection}` is the short name declared in the manifest (e.g., `invoices`). The core resolves the full namespaced collection path from the plugin token — the plugin never specifies the namespace in the request.

## What the Core Does on Every Call

On every storage request, the core performs these steps before touching the database:

1. Authenticates the plugin token in the `Authorization` header. Returns `401` if the token is missing, expired, or invalid.
2. Resolves the plugin's namespace from the token claims (e.g., `acme-billing` → `plugin_data.acme-billing`).
3. Looks up the registered JSON Schema for `{collection}` from the plugin's registration record.
4. Validates the request body against the schema for write operations. Returns `422` with field-level errors if validation fails.
5. Executes the MongoDB operation against the namespaced collection (`plugin_data.{plugin_id}.{collection}`).
6. Returns the result to the plugin.

Plugins never construct a database connection, never see MongoDB URIs, and never manage their own credentials.
