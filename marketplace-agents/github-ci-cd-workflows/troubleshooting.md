---
description: Common problems with GitHub CI/CD Workflows and how to fix them.
---

# Troubleshooting and FAQ

## Common problems

| What you see | What it means | What to do |
| --- | --- | --- |
| **"Could not resolve a GitHub token for the selected scope. Pick a GitHub source-control scope whose credential holds an access token."** | The scope has no usable access token. | Choose a GitHub source-control scope, and check that its credential holds a token. |
| **The Repository list is empty, or "Could not list repositories for this scope."** | The token cannot see any repositories, has expired, or the GitHub address is wrong. | Check the token's repository access and expiry, and for GitHub Enterprise Server check the scope's Account ID (see [Set Up](set-up.md)). |
| **"No workflows found in this repository."** | The repository has no workflows, or the token cannot read them. | Add a workflow, or give the token Actions read access. |
| **"This workflow does not declare `on: workflow_dispatch`, so it can't be triggered manually."** | GitHub only allows manual triggers for workflows with that setting. | Add `workflow_dispatch:` to the workflow's `on:` section on the branch you want to run. |
| **The trigger fails with an HTTP 422 message** | GitHub rejected the trigger, for example the workflow file does not exist on that branch or a required input is missing. | Check that the workflow exists on the chosen branch and that the inputs match. |
| **The trigger fails with 401 or 403** | The token expired, was revoked, or lacks permission to run workflows. | Update the token on the scope and give it Actions read and write access (see [Set Up](set-up.md)). |
| **The run record is Complete but has no run number** | GitHub accepted the trigger but the run was not visible yet. | Open the run again after a moment. The number and status fill in when GitHub shows the run. |
| **Logs show "log appears once the job finishes"** | GitHub publishes log text only after a job finishes. | Watch the step status, and open the step again when the job is done. |
| **Approve and Reject are disabled, with "You are not a required reviewer."** | The GitHub account behind the scope is not a required reviewer for that environment. | Add the account as a reviewer in GitHub, or approve in GitHub. |
| **"GitHub rejected the review"** | GitHub refused the approval, for example because the run is no longer waiting. | Refresh the run and check it in GitHub. |
| **"GitHub upstream error"** | GitHub returned an error or was unreachable. | Retry. If it persists, check GitHub's status and the scope's address. |

<!-- VERIFY: the exact on-screen messages. Messages listed here are from the code; the 422, 401 and 403 rows come from the trigger step's error text (HTTP code plus the start of GitHub's reply). Confirm in QA with a bad token and a workflow without a manual trigger. -->

## FAQ

**Does it support workflows that are not manually triggered?** No. Only workflows with `on: workflow_dispatch`.

**Does deleting a run record delete it in GitHub?** No. Only the DuploCloud tracking record is removed.

**Who is shown as the person who started the run in GitHub?** The GitHub account behind the scope's token, not the individual DuploCloud user.

**Can I re-run or cancel a run?** Not here. Use GitHub.

**Does it work with GitHub Enterprise Server?** Yes, when the scope's Account ID is the server's host name (see [Set Up](set-up.md)).

**Can someone else approve my run?** Any DuploCloud user who can open the run page can, if the token's account is a required reviewer. See [Permissions and Safety](permissions-and-safety.md).

<!-- VERIFY: FAQ is a first guess from the code. Kalpesh to add the questions customers actually ask. -->
