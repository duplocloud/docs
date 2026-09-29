---
description: Install published extensions, and build your own.
---

# Extensions

Extensions add capabilities to the platform — API resources, menu entries, and skills — loaded at runtime without redeploying the portal. There are two places to work with them, and they do different jobs:

| | Where | What it's for |
|---|---|---|
| **Extensions** (registry) | **AI Admin → Extensions** | Install and manage published extensions across the platform |
| **Extension Studio** | **Studio** within a workspace | Build a new extension from a description |

Start with the registry — installing something that already exists needs no source control and no build.

---

## Installing an extension

Go to **AI Admin → Extensions**. The page has two tabs: **Installed Extensions** and **Extension Library**.

### Installed Extensions

Summary tiles across the top show how many extensions are installed, how many API resources they contribute, how many need attention, and when the set last changed. The table below lists each one with its extension id, version, status, resource count, the menus it adds, and whether it is tracked in source control.

![Installed Extensions](../../.gitbook/assets/extensions-registry-step-01-registry-installed.png)

Use the **All statuses / Active / Disabled / Failed** filters to narrow the list — **Failed** is the one to check when an extension's resources or menus aren't appearing.

### Extension Library

The **Extension Library** tab is the catalog of extensions available to install. Each entry shows its category, a short description, and whether it is **Available** or already **Installed**.

![Extension Library](../../.gitbook/assets/extensions-registry-step-02-extension-library.png)

Click **Install** to add one, **Details** to read more first, or the link icon to open its source repository on GitHub. Versions come from the source repository's releases, so you can install a specific version rather than only the latest. **Refresh** re-reads the catalog.

### Inspecting an installed extension

Opening an installed extension shows what it actually contributes to the platform.

![Extension detail](../../.gitbook/assets/extensions-registry-step-03-catalog-entry-detail.png)

The header carries its status, extension id, version, and last-updated time. Below that:

* **Load Context** — the fully-qualified identifier and version the platform loaded
* **Source Control** — the repository it is tracked in, or **Not tracked** for a zip upload
* **Menu Entries** — how many navigation entries it adds
* **Skills** — the skills it registers, with their fully-qualified paths
* **Resources** — the API resources it registers, by origin type, sub-type, and REST segment

Three tabs give more detail: **Overview** (above), **Menu** (the navigation entries it adds), and **Manifest** (the raw declaration).

The **Actions** menu on the detail page lets you **Disable** an extension without removing it — its resources and menus stop loading, and the status changes to Disabled — or **Enable** one that is currently disabled. Both ask for confirmation first.

### Registering an extension from a file

If an extension isn't in the catalog, click **Register** and upload its `extension.zip`.

![Register extension](../../.gitbook/assets/extensions-registry-step-04-register-modal.png)

Extensions registered this way show **Not tracked** under Source Control, since there's no repository behind them.

---

## Building an extension in Extension Studio

Extension Studio is the authoring side, scoped to a workspace rather than the platform. Go to **Studio** in the workspace navigation.

Click **New Extension** and provide:

* **Extension name** and an **Icon**
* **GitHub Scope** — the source-control scope the extension's code is written to. This is required; Studio builds into a repository
* **Extra scopes** _(optional)_ — any further credentials the extension needs
* **Use source control** — whether to track the extension in the selected repository
* **Requirements** — a description of what the extension should do

Clicking **Create & Build** starts an agent that writes the extension against your requirements. You can **Preview** the generated result and step **Back** to revise before building.

Once built, an extension in Studio has two further actions on its detail page:

* **Load** — loads the built extension into the platform so its resources, menus, and skills become available
* **Deprovision** — tears the extension back down, removing what it contributed

{% hint style="info" %}
Extension Studio needs a GitHub scope because it builds into a repository. If you only want to use an extension someone else has published, install it from the **Extension Library** instead — that needs no source control.
{% endhint %}

---

## Which one should I use?

* **Install from the Extension Library** when the capability already exists. No build, no repository, no scope.
* **Register a zip** when you have a built extension that isn't published to the catalog.
* **Build in Extension Studio** when you need something that doesn't exist yet and are prepared to maintain it in your own repository.

For the concepts behind extensions — the plugin architecture, manifests, storage, and lifecycle — see the [Extension Framework](../extension-framework/README.md).
