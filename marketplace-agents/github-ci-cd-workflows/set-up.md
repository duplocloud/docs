---
description: What you need before you start, how to activate GitHub CI/CD Workflows from the Agent Marketplace, and how to connect it to your accounts.
---

# Set Up

## Before you start

- A **GitHub source-control scope** attached to your workspace. Its credential must hold an access token (a personal access token, a fine-grained token or an OAuth token). GitHub CI/CD Workflows acts on GitHub as the owner of that token.
- A workflow in the repository that declares **`on: workflow_dispatch`**, on the branch you want to run. Without it GitHub rejects the trigger.
- **Permissions** for the people who will use it (see [Permissions and Safety](permissions-and-safety.md)).

{% hint style="info" %}
Use a dedicated GitHub account, or a fine-grained token limited to the repositories you want to automate. Everyone who can use the scope in DuploCloud acts through that one GitHub identity.
{% endhint %}

### Which GitHub address it uses

| Scope setting | Address used |
| --- | --- |
| Account ID is empty, or a plain name such as `my-org` | `api.github.com`. A plain name is treated as the organization whose repositories are listed first. |
| Account ID is a host name (for example `github.mycompany.com`) | GitHub Enterprise Server at `https://<host>/api/v3`. |

If the organization lists no repositories, the list falls back to the repositories of the token's own user.

<!-- VERIFY: the exact scope fields in the DuploCloud console (provider type "github", "Account ID") and how a customer creates a GitHub scope. Screenshot GH-03. -->

### GitHub token permissions

The repo says the token needs `actions` and `contents` read access plus permission to dispatch workflows. It does not list fine-grained permission names. Based on what the code calls, the repository permissions below are the likely minimum.

| Feature | GitHub repository permission (fine-grained token) |
| --- | --- |
| List repositories and branches | Metadata: Read (always included); Contents: Read |
| Read a workflow's inputs | Contents: Read |
| List workflows, run status, jobs and logs | Actions: Read |
| Trigger a run | Actions: Read and write |
| Approve or reject a deployment | Deployments: Read and write, and the token's GitHub user must be a required reviewer on the environment |

For classic personal access tokens, the `repo` and `workflow` scopes.

<!-- VERIFY: permission names above are inferred from the GitHub REST endpoints the code calls (repos, branches, contents, actions/workflows, actions/runs, job logs, workflow dispatches, pending_deployments). They are not stated in the repo. Test a fine-grained token with exactly these permissions against a test repository and correct the table. Also confirm the classic scopes and whether organization approval of fine-grained tokens is needed. -->

## Activate GitHub CI/CD Workflows

1. Open the **Agent Marketplace** and find **GitHub CI/CD Workflows**.
2. Select **Activate** and confirm.
3. When it finishes, **GitHub Actions** appears under the **CI/CD** section of the menu.

<!-- VERIFY: marketplace steps, button names and the listing name. The repo's manifest calls the extension "GitHub Actions Trigger"; the stub name is "GitHub CI/CD Workflows". Menu path CI/CD > GitHub Actions is from the manifest. Screenshots GH-01 and GH-02. -->

## Grant access

Give the people who will use it the permissions described in [Permissions and Safety](permissions-and-safety.md), and make sure they can use the GitHub scope in the workspace.

<!-- VERIFY: the extension defines no permissions of its own. Which platform permission lets someone list, create and view these runs is inherited from the platform and is not in this repo. Confirm with the owner. -->

Next: [Use](use.md).
