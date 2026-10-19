# Connecting GitHub to DuploCloud

This guide walks through adding GitHub as a Source Control provider in DuploCloud, configuring credentials (a Personal Access Token or a GitHub App), creating a scope, and querying GitHub repositories through the AI agent.

---

## Step 1 — Navigate to the Source Control Providers

Switch to **AI Admin** using the product selector at the top of the left sidebar. Then go to **Workspaces** → **Providers** and click the **Source Control** tab. This lists every source control provider connected to your account.

![Source Control providers list](../../.gitbook/assets/github-step-02.png)

---

## Step 2 — Add a New Provider

Click **+ Add Provider**. Fill in the provider details:

- **Name** — a name to identify this provider
- **Type** — select **GitHub**
- **GitHub Hostname** — the URL of your GitHub instance:
  - **GitHub App credentials** — enter `https://github.com`
  - **Personal Access Token credentials** — `github.com` (the default) works
  - **GitHub Enterprise** — enter your custom hostname instead (e.g. `https://github.company.com`)

{% hint style="warning" %}
If you plan to use a **GitHub App** credential, the hostname must be `https://github.com`, including the `https://` prefix.
{% endhint %}

![Add Provider form](../../.gitbook/assets/github-step-03.png)

Click **Next**.

---

## Step 3 — Add Credentials

Enter a **Name** for the credential, then choose a **Credential Type**:

- **Personal Access Token** — authenticates as a GitHub user with a long-lived token.
- **GitHub App** — authenticates as a GitHub App installed on your organization. DuploCloud mints a short-lived (one hour) installation token for every request, and the App's private key is never passed to the agent. Recommended for organizations.

![Credential Type dropdown](../../.gitbook/assets/github-app-credential-type.png)

{% tabs %}
{% tab title="Personal Access Token" %}
Fill in:

- **API Key** — your GitHub Personal Access Token (starts with `ghp_`)
- **Credential Fields** — click **+ Add Credential Field** and add **Username** with your GitHub username

> **Where to find these values:** Create a Personal Access Token in GitHub under **Settings → Developer settings → Personal access tokens**. Select the repository scopes your agent needs — at minimum `repo` for private repositories, or `public_repo` for public only. The username is your GitHub handle shown in your profile URL (`github.com/<username>`).

![Personal Access Token credential](../../.gitbook/assets/github-step-06.png)
{% endtab %}

{% tab title="GitHub App" %}
Before you start, create and install a GitHub App by following [Creating a GitHub App](#creating-a-github-app) below. Then fill in:

- **App ID** — the numeric App ID shown on the App's **General** settings page
- **Installation ID** — the numeric ID of the App's installation on your organization. See [Find the Installation ID](#creating-a-github-app).
- **Private Key** — paste the full contents of the `.pem` file you downloaded from GitHub, including the `-----BEGIN RSA PRIVATE KEY-----` and `-----END RSA PRIVATE KEY-----` lines. Both PKCS#1 (`BEGIN RSA PRIVATE KEY`) and PKCS#8 (`BEGIN PRIVATE KEY`) formats are accepted.

![GitHub App credential](../../.gitbook/assets/github-app-credential.png)

{% hint style="info" %}
When editing an existing GitHub App credential, leave **Private Key** blank to keep the stored key.
{% endhint %}
{% endtab %}
{% endtabs %}

Click **Next**.

---

## Step 4 — Add a Scope

Fill in the scope details. The **Credential** is set to the one you created in the previous step.

- **Name** — a label for this scope
- **Repository Names RegEx** *(optional)* — a regex pattern to restrict which repositories the agent can access (e.g. `^duplocloud-.*`). Enter `.*` to allow every repository.
- **Branch Names RegEx** *(optional)* — a regex pattern to restrict which branches the agent can access (e.g. `^main$`). Enter `.*` to allow every branch.

{% hint style="warning" %}
**Leaving the RegEx fields blank:** Skill and Project git-sync deny every repository and branch when these fields are blank. For **GitHub App** credentials, a blank **Repository Names RegEx** still gives the agent's token access to **every repository the App is installed on**. When set, the token is limited to the matching repositories.
{% endhint %}

![Add Scope form](../../.gitbook/assets/github-step-08.png)

Click **Create**. DuploCloud creates the provider, credential, and scope together.

### Restrict GitHub App permissions *(optional)*

For **GitHub App** credentials, a scope can restrict any of the App's write permissions to read-only. Permissions are loaded from the App installation, so set them after the scope exists:

1. Open the provider, and on the **Scope** tab click the **⋮** menu next to your scope, then **Edit**.
2. Under **Permissions**, turn on **Restrict "\<permission\>" to read-only** for each permission the agent should only read. Permissions the App already grants as read-only are listed with a lock icon.
3. Click **Update**.

A scope can only narrow what the App installation was granted, never add to it. To grant a new permission, update the App's permissions in GitHub.

![Scope permissions for a GitHub App credential](../../.gitbook/assets/github-app-scope-permissions.png)

---

## Step 5 — Use GitHub in a Ticket

Go to **AI DevOps** → **HelpDesk** → **Add Ticket**. Select **generic-agent** as the agent and choose your GitHub scope from the scope dropdown.

![Scope dropdown with GitHub scope selected](../../.gitbook/assets/github-step-11.png)

Enter your request — for example, asking the agent to list your repositories. Click **Create Ticket**.

![Ticket ready to submit](../../.gitbook/assets/github-step-12.png)

---

## Step 6 — Agent Queries GitHub

The agent connects to GitHub using the scope credentials and retrieves the requested information.

The response lists your most recent repositories with details — name, visibility (public or private), and last updated date — along with an offer to take further action on any of them.

![GitHub repository results](../../.gitbook/assets/github-step-13.png)

---

## Creating a GitHub App

Use this section when you choose the **GitHub App** credential type in Step 3. You need to be an owner of the GitHub organization (or have the GitHub App manager role) to create and install the App.

{% stepper %}
{% step %}
### Create the App

In GitHub, go to your organization's **Settings** → **Developer settings** → **GitHub Apps** and click **New GitHub App**. Fill in:

- **GitHub App name** — `DuploCloud`
- **Homepage URL** — any URL, e.g. your DuploCloud portal URL
- **Callback URL** — leave blank. DuploCloud doesn't use the OAuth user flow.
- **Webhook** — clear the **Active** checkbox. DuploCloud doesn't receive webhooks.
- **Where can this GitHub App be installed?** — select **Only on this account**
{% endstep %}

{% step %}
### Set repository permissions

Under **Permissions** → **Repository permissions**, grant only what your agents need. A typical starting point:

| Permission | Access | Used for |
| --- | --- | --- |
| Metadata | Read-only | Required. Listing the repositories the App can access |
| Contents | Read and write | Cloning and browsing code, Skill/Project git-sync, pushing branches (use Read-only if agents shouldn't push) |
| Pull requests | Read and write | Opening and reviewing pull requests |
| Actions | Read-only | Troubleshooting GitHub Actions workflow runs |
| Checks | Read-only | Reading check run results on commits and pull requests |
| Commit statuses | Read-only | Reading commit status results |

Add **Issues** (Read and write) if agents should read or comment on issues.

You can make the access tighter for an individual scope later with the scope's **Permissions** setting, but a scope can never get more than the App grants here.

Click **Create GitHub App**.
{% endstep %}

{% step %}
### Copy the App ID and generate a private key

On the App's **General** page, copy the **App ID**.

In the App's left menu, click **Credentials**, then open the **Key pairs** tab and click **Generate a private key**. GitHub downloads a `.pem` file. Store it securely, because GitHub doesn't keep a copy.
{% endstep %}

{% step %}
### Install the App on your organization

In the App's left menu, click **Install App**, then click **Install** next to your organization. Choose **All repositories** or **Only select repositories**, then click **Install**.

{% hint style="info" %}
The agent can only reach repositories the App is installed on. To grant access to more repositories later, update the installation in GitHub. No changes are needed in DuploCloud.
{% endhint %}
{% endstep %}

{% step %}
### Find the Installation ID

The Installation ID isn't shown as a field anywhere in GitHub. It's the number at the end of the installation's settings URL. To find it:

1. Go to your GitHub organization's page (`https://github.com/<org>`) and click **Settings**.
2. In the left sidebar, under **Third-party Access**, click **GitHub Apps**.
3. Find your App in the **Installed GitHub Apps** list and click **Configure**.
4. Look at the browser's address bar. The URL looks like this:

   ```text
   https://github.com/organizations/<org>/settings/installations/12345678
   ```

   The number at the end (`12345678` in this example) is the **Installation ID**.

{% hint style="info" %}
Right after you install the App in the previous step, GitHub opens this same page, so you can copy the Installation ID from the address bar then.
{% endhint %}
{% endstep %}

{% step %}
### Add the credential in DuploCloud

Return to Step 3, select **GitHub App** as the **Credential Type**, and enter the **App ID**, **Installation ID**, and **Private Key**.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
**GitHub Enterprise Server:** create the App the same way on your GitHub Enterprise instance, and set the provider's **GitHub Hostname** (Step 2) to your Enterprise host (e.g. `https://github.company.com`). DuploCloud calls the API at `https://<host>/api/v3/`.
{% endhint %}

### Troubleshooting

| Error mentions | Fix |
| --- | --- |
| `verify private_key is a valid PEM-encoded RSA private key` | Paste the entire `.pem` file contents, including the `BEGIN` and `END` lines. Generate a new key if the file was altered. |
| `Verify the App is still installed and installation_id is correct` | Confirm the App is still installed on the organization and that the Installation ID matches the installation URL. |
| `missing app_id and/or installation_id` | Edit the credential and fill in both **App ID** and **Installation ID**. |
| `RepositoriesRegEx matched none of the ... repo(s)` | The scope's **Repository Names RegEx** matches no repositories the App is installed on. Fix the regex or add the repositories to the App installation. |
