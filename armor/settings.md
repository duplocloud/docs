# Settings

The **Settings** section holds two platform-wide admin stores: **System Settings** (arbitrary, typed configuration values) and **Global Secrets** (arbitrary name/value secrets available platform-wide).

## System Settings

A System Setting is a name/type/value entry — not a fixed list. A small set of known settings (e.g. a LangFuse observability URL) show up as ready-made templates, but admins can also define any custom setting a workspace or the platform needs to read.

Go to **AI Admin → Settings → System Settings**.

![System Settings, empty](../../.gitbook/assets/settings-step-01-system-settings-empty.png)

Click **+ Add** and fill in:

* **Type\*** — **String**, **Number**, **Bool**, or **JSON**
* **Setting\*** — pick one of the predefined settings, or **Custom Setting** to define your own
* **Name\*** — required for a custom setting; letters, numbers, `.`, `_`, `-` only
* **Value\*** — the input control matches the chosen Type (text field, number field, toggle, or a JSON editor)
* **Labels** (optional) — free-form tags for grouping related settings
* **Description** (optional)

![Add System Setting form, empty](../../.gitbook/assets/settings-step-02-add-setting-empty.png)

![Add System Setting form, filled in](../../.gitbook/assets/settings-step-03-add-setting-filled.png)

![System Setting added](../../.gitbook/assets/settings-step-04-setting-added.png)

{% hint style="info" %}
Settings created here are platform-wide (**Global** scope). A separate **Workspace Settings** page, available within a workspace's own settings, lets you define a same-named setting scoped to just that workspace — it overrides the global value for that workspace only, the same override pattern used by [LLM Mappings](agents/llm-models.md#llm-mappings) and [Quotas](access-control/quotas.md).
{% endhint %}

### Predefined settings

These appear in the **Setting** dropdown rather than needing a custom name. Anything not listed here can still be added as a **Custom Setting**.

| Setting | Type | Default | What it does |
|---|---|---|---|
| **Hidden Menu Items** | JSON | — | Sidebar menu item ids to hide, as a YAML list. A parent disappears once all of its children are hidden. Applies on the next page reload. |
| **Hidden Header Icons** | JSON | all shown | Navbar icons to hide, as a YAML map of icon id to flag. Recognised ids are `faults-notification-non-admin`, `trust-center`, and `help`. |
| **Hide Single Workspace Selector** | Bool | `false` | Hides the Workspace dropdown for users who only have one workspace. |
| **Workspace Memory Default (New Tickets)** | Bool | `true` | The starting state of the **Workspace Memory** toggle on a new ticket. |
| **Collapse Advanced Options (Add Helpdesk Ticket)** | Bool | — | Collapses the Advanced Options section by default when creating a ticket. |
| **Disable Product Analytics** | Bool | — | Stops asking users for analytics consent and collects nothing. Users are asked for consent by default. |
| **Allow kubectl/kubeconfig for static-token Kubernetes scopes** | Bool | off | Enables `kubectl` and **Download kubeconfig** for scopes backed by a static, long-lived credential. Off by default, because those credentials never expire on their own. |
| **LangFuse URL** | String | — | Base URL of the LangFuse instance embedded on the **Observability → LangFuse** page. |

{% hint style="info" %}
**Hidden Menu Items** and **Workspace Memory Default** can be set globally or per workspace; the rest are platform-wide only. A workspace value **replaces** the global one rather than merging with it.

The `-non-admin` suffix on a header icon id is load-bearing: `faults-notification-non-admin` hides that icon from User-role users only, never from administrators.
{% endhint %}

## Global Secrets

Global Secrets are name/value pairs available platform-wide — distinct from [Provider](providers/README.md) credentials, which are tied to a specific cloud/tool integration. A Global Secret is just a value your agents can reference, merged in alongside any Workspace-, Project-, or Ticket-level secrets.

Go to **AI Admin → Settings → Global Secrets**.

![Global Secrets, empty](../../.gitbook/assets/settings-step-05-global-secrets-empty.png)

Click **+ Add** and fill in:

* **Key\*** — the secret's name; cannot be changed after creation
* **Value\*** — the secret value; hidden by default, with a show/hide toggle

![Add Secret form, empty](../../.gitbook/assets/settings-step-06-add-secret-empty.png)

![Add Secret form, filled in](../../.gitbook/assets/settings-step-07-add-secret-filled.png)

![Secret added, value masked](../../.gitbook/assets/settings-step-08-secret-added-masked.png)

{% hint style="info" %}
Once saved, a secret's value is always masked in the list and API responses — only the last few characters are shown. If a Workspace, Project, or Ticket defines a secret with the same key, that more specific value takes precedence over the Global one.
{% endhint %}
