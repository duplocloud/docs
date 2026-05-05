# Plugin Architecture

This reference documents the technical contract between the Extension Framework core and plugin services. It covers the two contracts a plugin must implement, the registration flow, storage namespacing, authentication tokens, and lifecycle states.

## The Mental Model

Think of the core platform as an operating system and plugins as applications. The OS provides four things: a window manager (the UI shell and menu system that renders plugin views inside a consistent frame), a filesystem (namespaced storage with schemas, accessible through a generic HTTP API), an identity service (user authentication, JWT issuance and verification), and a package manager (registration, health checking, versioning, and lifecycle management).

The applications — plugins — provide their own logic, their own UI fragments (HTML or iframes), and a declaration of what menus they want and what data they need. The plugin has no knowledge of other plugins, no direct database access, and no involvement in routing or permission enforcement.

The core owns everything shared: identity, routing, the UI shell, and persistence. The plugin owns everything specific to its domain: business logic, API routes, and the transformation of data into HTML fragments the core renders.

A plugin can be written in any language. It only needs to speak HTTP and follow the manifest contract.

## The Two Contracts

Everything in this architecture flows from two contracts the core defines and the plugin implements.

**Contract A — What the plugin exposes (inbound):** The plugin must serve the HTTP routes it declared in its manifest. Each route corresponds to a menu view (`GET`, returns an HTML fragment) or an action (`POST`/`PUT`/`PATCH`/`DELETE`, processes form input and returns an HTML fragment). The plugin must verify the JWT the core sends with every request.

**Contract B — What the plugin consumes (outbound):** The plugin calls back to the core's storage API to persist and read data. It uses a plugin token issued at registration. It can only touch its own namespaced collections.

Everything else — menu rendering, user routing, permission checks, schema validation, tenant isolation — is the core's responsibility.

## Reference Pages

- [Manifest and Registration](manifest-and-registration.md) — the manifest format and what the core does at install time
- [Storage API](storage-api.md) — namespace convention, endpoints, and per-call processing
- [Authentication](authentication.md) — the three tokens, their boundaries, and the runtime flow
- [Lifecycle States](lifecycle-states.md) — state machine, state descriptions, and storage access per state
- [Schema Versioning](schema-versioning.md) — compatible vs. breaking changes, migration handlers, and uninstall policies
