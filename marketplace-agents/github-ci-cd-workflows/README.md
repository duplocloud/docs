---
description: Start, approve and follow GitHub Actions workflow runs from DuploCloud.
icon: robot
---

# GitHub CI/CD Workflows

Start your GitHub Actions workflows from DuploCloud and follow each run until it finishes, without needing access to GitHub yourself. You pick a repository, a workflow and a branch, fill in the workflow's inputs, and start the run. DuploCloud permissions decide who can start runs, who can approve them and who can read the logs.

{% hint style="warning" %}
GitHub CI/CD Workflows starts real workflow runs in your repositories and can approve GitHub deployment gates. GitHub sees every action as the account that owns the GitHub scope's token. DuploCloud records which user actually did it. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

## What it does

1. **Starts runs.** Any workflow that declares `on: workflow_dispatch`, on a repository and branch your GitHub scope allows. The input form is built from the workflow file.
2. **Holds runs on protected branches.** If the branch has GitHub branch protection, nothing is sent to GitHub until a second person approves the run in DuploCloud. The approved run uses exactly the commit that was requested.
3. **Reviews GitHub deployment gates.** When a run waits on a protected GitHub environment (for example `production`), approvers can approve or reject it from DuploCloud.
4. **Follows each run.** Live status, each job and step, and the log text for users allowed to read logs.
5. **Explains failures.** A failure summary names the job, the step and a likely cause. **Debug with AI** opens an AI helpdesk chat that investigates the failure without changing anything.
6. **Measures.** A metrics page shows usage, success rate, approval wait, run time and anomalies for the workspace.
7. **Manages approvers.** Administrators choose who can approve runs on the **GitHub Actions Settings** page.

Nobody can approve a run they requested themselves. This applies to administrators too.

## Who it is for

- **Developers** who start builds and deployments.
- **Approvers** who release runs on protected branches and review deployment gates.
- **Administrators** who connect GitHub, limit what can be run, and choose approvers.

## Where to find it

Under **CI/CD** in the left menu:

| Menu item | What it is | Who sees it |
| --- | --- | --- |
| **GitHub Actions** | The run list. Start runs and open any run. | Anyone who can read runs |
| **GitHub Actions Metrics** | Usage and health numbers for the workspace. | Anyone who can read runs |
| **GitHub Actions Settings** | Choose who can approve runs. | DuploCloud administrators only |

Everything is per workspace.

## What it works with

| | |
| --- | --- |
| Source control | GitHub (github.com) and GitHub Enterprise Server |
| Workflows | GitHub Actions workflows that declare `on: workflow_dispatch` |
| Credential | A GitHub source-control scope attached to the workspace, holding an access token |
| Not covered | Starting runs from other triggers (push, pull request, schedule), cancelling or re-running a run, editing workflows, managing GitHub environments or secrets, and other CI systems. Do those in GitHub. |

<!-- VERIFY: free or paid. Not in the code; decided by the Marketplace listing. -->

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need, how to activate the agent, connect GitHub, limit what can be run, and choose approvers. |
| [Use](use.md) | Start a run, find and follow runs, approve runs and deployment gates, investigate failures, and read the metrics. |
| [Permissions and Safety](permissions-and-safety.md) | What the agent can read and change, what needs approval, and what read-only users, regular users, approvers and administrators can do. |
| [Troubleshooting and FAQ](troubleshooting.md) | Error messages and how to fix them. |
