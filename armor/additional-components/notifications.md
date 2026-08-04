# Notifications

Portal notifications are configured in two places: an **SMTP provider** (the credentials for sending mail) under **Providers**, and **Notifications** (which use case gets routed to which provider) under its own top-level section.

## Adding an SMTP Notification Provider

Go to **Providers**, select the relevant Provider group, then open the **Notifications** tab — a category alongside Cloud, Kubernetes, Observability, Incident Management, Source Control, and GRC.

![Notifications provider tab, empty](../../../.gitbook/assets/notifications-step-01-empty-tab.png)

Click **Add** and follow the same **Provider Details → Credentials → Scope** flow described in [Providers](../providers/README.md#adding-providers-and-defining-scopes). **SMTP** is currently the only notification provider type.

![Provider Details step — Type set to SMTP](../../../.gitbook/assets/notifications-step-02-provider-details.png)

On the **Credentials** step, fill in:

* **Name\*** — a label for this credential
* **SMTP Host\*** — the mail server hostname
* **Port\*** — the SMTP port (commonly `587`)
* **From Address\*** — the address mail is sent from
* **Username\*** and **Password\*** — SMTP auth credentials

![SMTP credential fields filled in](../../../.gitbook/assets/notifications-step-03-smtp-credentials.png)

Finish the **Scope** step as with any other Provider, then attach it to the relevant Workspace(s).

![Attach Scope to Workspaces](../../../.gitbook/assets/notifications-step-04-attach-workspace.png)

## Routing Notifications to a Provider

Go to **Notifications** in the sidebar. This page lists each notification **use case** and how many channels are configured for it.

![Notifications use case list](../../../.gitbook/assets/notifications-step-05-use-cases-list.png)

Click a use case to open it, then **+ Add Channel**.

![Use case detail, no channels configured](../../../.gitbook/assets/notifications-step-06-use-case-empty.png)

For each channel, set:

* **Enabled** — toggle the channel on or off without removing it
* **From Identity** (optional) — overrides the SMTP provider's From Address for this use case
* **Provider\*** — the SMTP provider to send through

![Channel filled in with a provider and From Identity](../../../.gitbook/assets/notifications-step-07-add-channel-filled.png)

Click **Save**.

![Use case list showing 1 enabled channel](../../../.gitbook/assets/notifications-step-08-channel-saved.png)

{% hint style="info" %}
A use case with no enabled channel simply doesn't send anything — there's no default or fallback provider. Today there's a single use case, **New User Welcome**, sent automatically whenever a new user is created; more use cases will appear here as they're added, with no configuration needed to make them show up.
{% endhint %}
