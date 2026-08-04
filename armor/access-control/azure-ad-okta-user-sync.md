# Azure AD & Okta User Sync

User Sync provisions and deprovisions HelpDesk user accounts directly from your Azure AD or Okta directory, instead of an admin adding each [User](users.md) by hand.

{% hint style="info" %}
This is distinct from **Microsoft SSO Login** — SSO controls how a user authenticates; User Sync controls whether their account and group membership exist in HelpDesk in the first place. They're independent features, though for Azure AD both happen to reuse the same app registration credentials.
{% endhint %}

## How it works

DuploCloud polls your directory on a timer rather than exposing an endpoint for your IdP to push to — it reads two specific group names from Azure AD (via Microsoft Graph) or Okta (via Okta's Groups API):

* **`HelpDesk-Admin`** — members are synced in as HelpDesk Administrators
* **`HelpDesk-UG-<suffix>`** — members are synced in as regular Users, and added to a [User Group](user-groups.md) named `<suffix>`, which is created automatically the first time it's seen

Each sync pass:

* Creates an account for any group member not already in HelpDesk
* Updates a synced user's role and group membership to match current directory group membership
* Reactivates a previously-deactivated synced user if they reappear in a relevant group
* Deactivates a synced user who's no longer in any relevant group — this is a deactivation, not a deletion; their account and history are preserved

## What this doesn't touch

User Sync only manages accounts it created. A manually-created user is never modified or deactivated by sync, even if their email later shows up in one of the synced groups. In the Users list, an IdP-synced account shows a lock badge and can't be edited or deleted manually — to change a synced user's access, change their group membership in Azure AD/Okta instead.

## Setup

There's no in-app screen for connecting a directory — enabling and configuring User Sync (tenant/client credentials for Azure AD, domain and API token for Okta, and the sync interval) is a deployment-time setting, done by your DuploCloud ops contact rather than from within the product. It's off by default.
