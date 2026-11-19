---
description: Builds and runs GitHub CI/CD workflows for your repositories.
---

# GitHub CI/CD Workflows

Start your GitHub Actions workflows from DuploCloud, then watch each run without leaving the platform. You pick a repository, a workflow and a branch, fill in the workflow's inputs, and trigger the run. DuploCloud shows the live status, each job and step with its log output, and lets you approve or reject a run that is waiting on a protected GitHub environment.

{% hint style="warning" %}
GitHub CI/CD Workflows starts real workflow runs in your repositories, and can approve deployments to protected environments. Those actions are performed with the credential of the GitHub scope you choose. See [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

<!-- VERIFY: the repo has no role check of its own (no permission names, no approval gate in DuploCloud). Whether this is admin-only or open to users is the owner's decision (Kalpesh Suryawanshi, ClickUp 17twvjx4bm1). Confirm the warning and the audience once decided. -->

## What it does

1. **Lists your repositories** that the GitHub scope's credential can see (up to 500), in a searchable list.
2. **Lists the workflows** in the repository you choose (the first 100) and the branches for the branch picker (up to 500).
3. **Builds the form from the workflow.** The workflow's manual-trigger inputs are read from its definition file and shown as fields: a choice becomes a dropdown, a boolean a switch, anything else a text box.
4. **Triggers the run** on the branch or tag you choose, with your input values.
5. **Tracks the run.** The status and result (such as success or failure) are refreshed from GitHub each time you open the run.
6. **Shows logs.** A Logs tab lists each job and each step with its live status. Select a step to see its output.
7. **Handles approvals.** If the run is waiting for a protected environment, an approval banner lets you approve or reject it, with an optional comment.

A workflow can only be triggered from here if it declares `on: workflow_dispatch` (GitHub's manual trigger).

## Who it is for

Developers and DevOps engineers who run builds and deployments with GitHub Actions and want to start, monitor and approve them from DuploCloud.

<!-- VERIFY: audience wording is inferred from the extension README. Confirm with the owner, especially after the admin-only or user decision. -->

## What it works with

| | |
| --- | --- |
| Source control | GitHub (github.com) and GitHub Enterprise Server |
| Workflows | GitHub Actions workflows that declare `on: workflow_dispatch` |
| Credential | A GitHub source-control scope attached to your workspace, holding an access token |
| Not covered | Starting runs from other triggers (push, pull request, schedule), re-running or cancelling a run, and other CI systems |

<!-- VERIFY: free or paid. The repo does not say. The Release 1 listing and console decide this. -->
<!-- VERIFY: "Not covered" row: the code has no re-run, cancel or non-dispatch trigger. Confirm none are planned for the first release. -->

## In this section

| Page | What it covers |
| --- | --- |
| [Set Up](set-up.md) | What you need before you start, how to activate GitHub CI/CD Workflows from the Agent Marketplace, and how to connect it to your accounts. |
| [Use](use.md) | Step-by-step walkthroughs of the main things GitHub CI/CD Workflows does. |
| [Permissions and Safety](permissions-and-safety.md) | What GitHub CI/CD Workflows can read and change, which actions need approval, and how it behaves for read-only, regular and admin users. |
| [Troubleshooting and FAQ](troubleshooting.md) | Common problems with GitHub CI/CD Workflows and how to fix them. |
