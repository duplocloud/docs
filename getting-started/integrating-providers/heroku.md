# Heroku Integration

Connect a Heroku account as a provider so the DuploCloud agent can interact with your Heroku apps, dynos, and resources using your API credentials.

---

## Prerequisites — Retrieve Your Heroku API Token

You need a Heroku API token to authenticate the provider. You can retrieve it from the Heroku Dashboard or the Heroku CLI.

**From the Heroku Dashboard:**

1. Log in to [heroku.com](https://heroku.com) and go to **Account Settings**.
2. Scroll down to the **API Key** section.
3. Click **Reveal** to view your existing token, or **Regenerate API Key** to create a new one.
4. Copy the token.

**From the Heroku CLI:**

```bash
heroku login
heroku auth:token
```

Copy the token output — this is the value you will use in the **Credentials** step below.

---

## Step 1 — Navigate to Providers

Go to **AI Admin → Providers** and click the **Other** tab.

![](<../../.gitbook/assets/heroku-step-02.png>)

## Step 2 — Add the Provider

Click **+ Add**. Fill in the fields:

- **Name** — a label for this provider
- **Type** — select **Other**
- **Account ID** — enter `api.heroku.com`

Click **Create Provider**.

![](<../../.gitbook/assets/heroku-step-03.png>)

## Step 3 — Provider Created

The provider detail page opens with a success confirmation. The sidebar shows the Category, Type, and Account ID. Two tabs are available: **Scope** and **Credentials**.

![](<../../.gitbook/assets/heroku-step-04.png>)

## Step 4 — Add a Credential

Click the **Credentials** tab, then click **+ Add**. Fill in the modal:

- **Name** — a label for this credential
- **Credential Fields** — add a field with:
  - **Key** — `apitoken`
  - **Type** — `String`
  - **Sensitive** — enable this toggle so the token is stored encrypted
  - **Value** — your Heroku API token

Click **Create**.

![](<../../.gitbook/assets/heroku-step-05.png>)

## Step 5 — Add a Scope

Click the **Scope** tab, then click **+ Add**. Fill in the modal:

- **Name** — a label for this scope
- **Credential** — select the credential created in the previous step

Click **Create**.

![](<../../.gitbook/assets/heroku-step-06.png>)

## Step 6 — Verify the Connection

To confirm the provider is working, create a new ticket and select the Heroku scope from the scope picker.

![](<../../.gitbook/assets/heroku-step-08.png>)

The agent will use the Heroku credential to call the API. A successful response confirms the integration is active — the agent lists your Heroku apps along with their region, stack, and last updated date.

![](<../../.gitbook/assets/heroku-step-09.png>)
