# Setting Up a GCP Cloud Provider

The GCP Cloud Provider lets DuploCloud AI agents interact with your Google Cloud account — querying resources, running `gcloud` commands, and managing infrastructure on your behalf. Authentication uses a **Service Account** key.

---

## Step 1 — Create a Service Account Key in GCP

Before setting up the provider in DuploCloud, you need to generate a JSON key file from your GCP service account.

1. In the GCP Console, go to **IAM & Admin** → **Service Accounts**
2. Select an existing service account or create a new one
3. Click the service account → **Keys** tab → **Add Key** → **Create new key** → **JSON**
4. Click **Create** — GCP will download a JSON file to your machine

Open the downloaded JSON file. You will use three values from it when setting up DuploCloud:
- **`project_id`** — your GCP Project ID
- **`client_email`** — the service account email
- **`private_key`** — the full private key starting from `-----BEGIN RSA PRIVATE KEY-----`

> **Note:** The service account needs appropriate IAM roles assigned at the project level (e.g. **Viewer** for read-only access, or broader roles if the agent needs to create or modify resources).

---

## Step 2 — Add the GCP Provider

In DuploCloud, go to **Providers** in the left sidebar, select your tenant (e.g. **IT**), and click the **Cloud** tab. Click **+ Add**.

![Cloud providers list](../../.gitbook/assets/gcp-step-01.png)

Fill in the **Add Provider** form:

- **Name** — a name for this provider (e.g. `GCP-TEST`)
- **Type** — select `GCP`
- **Project ID** — your GCP project ID (found as `project_id` in the JSON key file)

Click **Create Provider**.

![Add Provider form](../../.gitbook/assets/gcp-step-02.png)

---

## Step 3 — Add a Credential

Click on your new provider to open it, then go to the **Credentials** tab and click **+ Add**.

The **Add Credential** form has two dedicated fields for GCP:

![Add Credential modal — empty](../../.gitbook/assets/gcp-step-03.png)

Fill in:

- **Name** — a name for this credential (e.g. `GCP-Test`)
- **Service Account Email** — the `client_email` value from the JSON key file
- **Service Account Password** — paste the full `private_key` value from the JSON key file, starting from `-----BEGIN RSA PRIVATE KEY-----` and including the closing `-----END RSA PRIVATE KEY-----` line

Click **Create**.

![Add Credential modal — filled](../../.gitbook/assets/gcp-step-04.png)

---

## Step 4 — Add a Scope

On the **Scope** tab, click **+ Add**.

- **Name** — a name for this scope (e.g. `GCP-test-scope`)
- **Credential** — select the credential you just created

Click **Create**. The scope appears in the list.

![Scope created](../../.gitbook/assets/gcp-step-05.png)

---

## Step 5 — Use the Scope in a Ticket

Go to **HelpDesk** and create a new ticket. In the scope selector, choose the GCP scope from the dropdown.

![Scope dropdown with GCP scope selected](../../.gitbook/assets/gcp-step-06.png)

Type your request and click **Create Ticket**.

![Ticket ready with GCP scope](../../.gitbook/assets/gcp-step-07.png)

---

## Step 6 — Output

The agent authenticates with GCP using the service account and executes the request. Results appear in the ticket thread.

![Agent output — GCP query results](../../.gitbook/assets/gcp-step-08.png)
