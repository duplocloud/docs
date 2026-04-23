# Integrating Jira with DuploCloud

Connecting Jira to DuploCloud lets the AI agent read tickets, create issues, update statuses, and act on Jira data on your behalf. You will need an Atlassian API token, your account email, and your Jira Cloud ID.

---

## Step 1 — Add the Jira Provider

In DuploCloud, go to **Providers** in the left sidebar, select your tenant (e.g. **IT**), and click the **Other** tab. Click **+ Add**.

![Other providers list](../../.gitbook/assets/jira-step-01.png)

Fill in the **Add Provider** form:

- **Name** — a name for this provider (e.g. `Jira-test`)
- **Type** — select `Other`
- **Account ID** — your Atlassian domain (e.g. `your-org.atlassian.net`)

Click **Create Provider**.

![Add Provider form](../../.gitbook/assets/jira-step-02.png)

The provider is created and you are taken to the provider detail page.

![Provider created successfully](../../.gitbook/assets/jira-step-03.png)

---

## Step 2 — Add a Credential

On the **Credentials** tab, click **+ Add**. Add the following credential fields:

- **`apikey`** — your Atlassian API token. Generate one at **id.atlassian.com** → **Security** → **API tokens** → **Create API token**. Set Sensitive to on.
- **`username`** — the email address associated with your Atlassian account
- **`CloudID`** — your Jira Cloud ID. To find it, navigate to `https://your-domain.atlassian.net/_edge/tenant_info` in your browser — the `cloudId` field in the response is the value to use here

Click **Create**.

![Add Credential with apikey, username, and CloudID](../../.gitbook/assets/jira-step-04.png)

---

## Step 3 — Add a Scope

On the **Scope** tab, click **+ Add**.

- **Name** — a name for this scope (e.g. `Jira-test-scope`)
- **Credential** — select the credential you just created

Click **Create**.

![Add Scope modal](../../.gitbook/assets/jira-step-06.png)

---

## Step 4 — Use the Scope in a Ticket

Go to **HelpDesk** and create a new ticket. In the scope selector, choose the Jira scope from the dropdown.

![Scope dropdown with Jira-test-scope selected](../../.gitbook/assets/jira-step-07.png)

Type your request and click **Create Ticket**.

![Ticket ready with Jira scope](../../.gitbook/assets/jira-step-08.png)

---

## Step 5 — Output

The agent authenticates with your Jira instance and executes the request. Results appear in the ticket thread.

![Agent reading and acting on Jira tickets](../../.gitbook/assets/jira-step-09.png)

![Both tickets transitioned to Done](../../.gitbook/assets/jira-step-10.png)
