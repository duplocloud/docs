# Schema Versioning

Every schema declaration in the manifest carries a version (via the top-level `version` field). The core stores all historical schemas, not just the latest. When a plugin is updated, the core compares the incoming version against the registered version and determines whether to apply the change automatically or require a migration handler.

## Compatible Changes

Compatible changes are applied automatically when the plugin submits an updated manifest. No migration handler is needed and the plugin does not enter `migrating` state.

Compatible changes include:

- Adding optional fields to an existing collection schema
- Widening enum values (adding new allowed values to an existing enum)
- Adding indexes to a collection

## Breaking Changes

Breaking changes require a migration handler registered alongside the schema update. The core will not apply a breaking schema change without one.

Breaking changes include:

- Removing fields from an existing collection schema
- Narrowing types (for example, changing a field from `string` to `enum` with a restricted set)
- Renaming collections

If the core detects a breaking change and no migration handler is registered, it rejects the update with a `409 Conflict` response and returns a diff of the conflicting fields.

## Migration Handlers

A migration handler is an HTTP endpoint the plugin declares alongside the schema update. When the core receives a manifest update that includes breaking changes:

1. The core moves the plugin to `migrating` state. Menus are hidden and storage is frozen.
2. The core calls the plugin's migration handler endpoint.
3. The plugin iterates over its existing documents and transforms them in place, calling the storage API (which accepts writes during migration from the migration handler context only).
4. When the handler returns `200`, the core applies the new schema, swaps the validator, and moves the plugin back to `active`.

If the handler returns a non-`200` response or times out, the plugin stays in `migrating` state and requires manual intervention from an administrator. Partial transformations are not automatically rolled back — the plugin is responsible for making its handler idempotent.

## Uninstall Policies

When a plugin is deregistered, the core applies an uninstall policy to determine what happens to the plugin's data. The policy is set by the administrator on a per-tenant basis. The plugin has no vote in this decision.

- **retain** — the plugin is removed from the registry and its menus disappear, but the namespaced collections remain in place. Data can be accessed directly by administrators.
- **archive** — the plugin's collections are moved to cold storage. Data is preserved but not queryable through normal means.
- **purge** — the plugin's namespaced collections are deleted. Data is not recoverable after purge completes.

The active uninstall policy for a plugin is visible in the admin console under the plugin's registration record.
