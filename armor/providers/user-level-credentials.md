# User-Level Credentials

A Scope's credential is normally shared by everyone who uses it — a team-level secret set on the Provider. **User-Level Credentials** let an individual user override that shared credential with their own, for a specific Scope, without affecting anyone else using the same Scope.

This is useful when different people need to act with their own identity against the same infrastructure — for example, each engineer using their own IAM role on a shared `aws-read-only` Scope instead of a single team credential.

## Adding a Personal Credential

Personal credentials are managed from your own **Profile**, not from the Providers admin pages.

### 1. Open Credential Overrides

Click your avatar in the top-right corner and select **Profile**. Go to the **Credential Overrides** tab.

![Credential Overrides tab, empty state](../../../.gitbook/assets/user-level-credentials-step-01-empty.png)

### 2. Select a scope

Click **Add Credential**. Choose the Scope you want to override from the list — it shows every Scope you have access to across your workspaces.

![Select Scope modal](../../../.gitbook/assets/user-level-credentials-step-02-select-scope.png)

Click **Continue**.

### 3. Fill in your credential

Give it a **Display Name**, then fill in the fields for the Scope's provider type:

- **AWS** — choose **Access Key** (Access Key ID + Secret) or **IAM Role** (Role ARN)
- **Kubernetes** — choose **Token**, **Cloud Role**, **Service Account**, or (on AKS) **Service Principal** / **Managed Identity**
- **Other providers** — the same credential fields the shared credential uses, plus any custom key/value pairs you need

![Add Personal Credential form](../../../.gitbook/assets/user-level-credentials-step-03-add-form.png)

Click **Create**.

### 4. It's active immediately

Your personal credential appears in the table and is used automatically on every ticket you run against that Scope — no per-ticket toggle needed.

![Personal credential added, shown in the table](../../../.gitbook/assets/user-level-credentials-step-04-added.png)

{% hint style="info" %}
* Your personal credential only affects **your own** tickets — other users on the same Scope keep using the shared credential (or their own override, if they've set one).
* Use the **Enabled** toggle to fall back to the shared credential without losing your saved values — disabling doesn't delete the credential.
* Any user with access to a Scope can add their own override for it; there's no additional admin permission required.
{% endhint %}
