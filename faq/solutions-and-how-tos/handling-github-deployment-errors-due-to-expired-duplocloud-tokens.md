# Handling GitHub Deployment Errors Due to Expired DuploCloud Tokens

When deploying applications via GitHub Actions, deployments can fail if the DuploCloud API token used for authentication has expired. This guide explains how to resolve the issue and prevent it from recurring.

### Step 1: Confirm the Cause of the Failure

Check your GitHub Actions workflow logs to verify that the deployment failure is due to an expired DuploCloud API token. Look for authentication errors referencing the token.

### Step 2: Generate a New API Token

Follow the instructions in the [DuploCloud API Tokens documentation](https://docs.duplocloud.com/docs/access-control/api-tokens#permanent-api-tokens) to generate a new token.

### Step 3: Update GitHub Secrets or Environment Variables

1. Open your GitHub repository settings.
2. Navigate to **Secrets and variables** → **Actions**.
3. Update the relevant secret or environment variable with the new API token.&#x20;

<table data-header-hidden><thead><tr><th width="211.111083984375">Field / Action</th><th>Description</th></tr></thead><tbody><tr><td><strong>Secret Name</strong></td><td>The name of the GitHub secret holding your DuploCloud token (e.g., <code>DUPLO_TOKEN</code>).</td></tr><tr><td><strong>Value</strong></td><td>Paste the newly generated DuploCloud API token.</td></tr></tbody></table>

### Step 4: Rerun the Workflow

Once the token is updated, rerun the failed GitHub Actions workflow to complete your deployment.

### Step 5: Prevent Future Token Expiration Issues

To avoid deployment interruptions:

<table data-header-hidden><thead><tr><th width="277.11114501953125">Action</th><th>Description</th></tr></thead><tbody><tr><td><strong>Set up token expiration alerts</strong></td><td>Monitor token expiration dates in advance.</td></tr><tr><td><strong>Use permanent API tokens</strong></td><td>Recommended for CI/CD automation to reduce the need for frequent updates.</td></tr></tbody></table>

[Learn how to set up token expiration alerts](https://docs.duplocloud.com/docs/access-control/api-tokens#permanent-api-tokens).
