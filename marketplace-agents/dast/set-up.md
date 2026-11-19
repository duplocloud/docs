---
description: What you need before you start, how to activate DAST from the Agent Marketplace, and how to add your first application.
---

# Set Up

## Before you start

- **An application you own and may test**, reachable by `http` or `https` URL. Prefer a staging or test environment.
- **A place for ZAP to run.** The scan runs OWASP ZAP in a Docker container on the agent's host. The host must be able to run Docker, pull the ZAP image from `ghcr.io`, and reach your application's URL.
- **Optional: an "other" scope** that holds a test login for the application, if you want to scan behind a login. Use a dedicated test account.
- **Optional: a GitHub scope** whose credential can read your repositories, and push branches and open pull requests if you want fixes. Only GitHub is supported.
- **Permissions** for the people who will use it (see [Permissions and Safety](permissions-and-safety.md)).

<!-- VERIFY: "the agent's host runs Docker" is taken from run-scan.sh ("Docker daemon not reachable from the agent"). Confirm what customers must provide in each deployment, and whether egress to ghcr.io is needed (the ZAP image is pulled on each run unless DAST_PULL=0 is set by the platform). -->
<!-- VERIFY: the pre-meeting review said a default Kubernetes scope should be mandatory in agent setup. Nothing in this repo (manifest, backend, forms, skills) references a Kubernetes scope or cluster. Confirm whether this is a platform-level setting and where it is configured, then add the step. -->

{% hint style="info" %}
DAST needs **no cloud (AWS, Azure or GCP) permissions**. The only credentials it uses are the optional application login scope and the optional GitHub scope.
{% endhint %}

<!-- VERIFY: the extension README names no IAM actions or provider roles, and the code requests none. Confirm that nothing else (for example a Kubernetes scope for the agent runtime) needs cloud permissions. -->

### Application login scope (optional)

The scope is an **other** provider credential. DAST reads these keys from it (key names are not case-sensitive):

| Key | Used for |
| --- | --- |
| `authType` | `form`, `json`, `bearer`, `header` or `none`. If missing, DAST infers it: a `token` means bearer, a `username` plus `password` means form login, otherwise no login. |
| `loginUrl` | Login page (form and JSON). A relative URL is resolved against the provider's account ID value. |
| `loginRequestUrl` | Where the login is posted, if it differs from `loginUrl`. |
| `username`, `password` | The test account (form and JSON). |
| `usernameField`, `passwordField` | Field names in the login request. Default `username` and `password`. |
| `loggedInRegex`, `loggedOutRegex` | Patterns ZAP uses to check that the session is still signed in. |
| `token`, `headerName` | Bearer token or header value (bearer and header). Default header `Authorization`. |

If you select a login scope that cannot be used (for example `authType` is `form` but there is no password), the scan stops and says which key names it found. It never falls back to an anonymous scan.

### GitHub scope (optional)

The scope's credential must be able to read the repositories you list. To raise fix pull requests it must also be able to push a branch and open a pull request.

<!-- VERIFY: exact GitHub permissions (token scopes or fine-grained permissions) for read, push and PR creation. The code only says "read the repositories (and push branches, for fix PRs)" and uses `gh pr create`. Customers need the precise list. -->

## Activate DAST

1. Open the **Agent Marketplace** and find **DAST**.
2. Select **Activate** and confirm.
3. When it finishes, the agent appears in the left menu under **Security** as **DAST (ZAP)**.

<!-- VERIFY: exact marketplace steps and button names (screenshots DA-01, DA-02). The menu path Security > DAST (ZAP) comes from manifest.json. -->

## Grant access

Give the people who will use it the permissions in [Permissions and Safety](permissions-and-safety.md). The **Fix DAST findings via pull request** action is granted separately; the "all" permission does not include it.

## Add your first application

1. Open **Security > DAST (ZAP)** and select **Add DAST Target**.
2. **Target** step:
   - **Name**: letters, digits and hyphens, 2 to 60 characters (for example `portal-staging`). It cannot be changed later.
   - **Application URL**: an absolute `http` or `https` URL.
   - **Default scan type**: Baseline (passive), Full (active) or API. Baseline is the default.
   - **API definition URL**: required for the API type.
   - **Max duration (minutes)**: 1 to 240. Default 30.
   - **Include paths** and **Exclude paths**: optional, one regular expression per line. Empty include paths scans the whole site. Exclude logout and destructive endpoints.
3. **Authentication** step: select **Scan as a signed-in user** and choose the scope that holds the login. Skip it to scan anonymously.
4. **Source code** step: select **Link the application's source code**, choose the GitHub scope and pick repositories (or type `org/repo`). You can also attach one or more **Architecture skills**: workspace skills that describe your application. Skip all of it to get triaged findings without code locations or fix pull requests.
5. **Review** the summary and select **Create**.

<!-- VERIFY: field names against the live form (screenshots DA-03 to DA-06). -->
<!-- VERIFY: the review said max duration is disabled for v1 and the advanced cluster option is disabled. The code still shows and validates Max duration (1 to 240) and has no cluster option. Confirm what the released UI shows, then edit this list. -->
<!-- VERIFY: nothing in the code checks that you own the application URL, and no ownership or domain verification step exists. The review said active scans require proof of domain ownership. Confirm where this is enforced (platform, a later release, or not yet built) and add the steps here. -->

Next: [Use](use.md).
