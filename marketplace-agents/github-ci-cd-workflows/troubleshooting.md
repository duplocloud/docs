---
description: Common problems with GitHub CI/CD Workflows and how to fix them.
---

# Troubleshooting and FAQ

## Error messages

| What you see | What it means | What to do |
| --- | --- | --- |
| **"GitHub rejected the scope's token (expired or revoked). Ask an admin to refresh the GitHub scope's credential."** | GitHub refused the token. | An administrator updates the token on the GitHub scope. |
| **"The scope's GitHub token does not have permission for this operation."** | The token lacks a GitHub permission. | Give the token the permissions in [Set Up](set-up.md). |
| **"The selected scope has no GitHub access token. Pick a GitHub source-control scope."** or **"The selected scope is not a GitHub source-control scope."** | The chosen scope is not a usable GitHub scope. | Pick a GitHub source-control scope whose credential holds a token. |
| **"The selected scope is not attached to this workspace or you cannot use it."** | The scope belongs to another workspace, or you have no access to it. | Pick another scope, or ask an administrator for access. |
| **"Repository '…' is not allowed by the selected scope."** or **"Ref '…' is not allowed by the selected scope."** | The scope's allow-list excludes it. | Pick an allowed repository or branch, or ask an administrator to change the allow-list. |
| **"This workflow does not declare 'on: workflow_dispatch', so it cannot be triggered."** | The workflow has no manual trigger. | Add `workflow_dispatch:` to the workflow's `on:` section on that branch. |
| **"This workflow is disabled in GitHub."** | The workflow is turned off in GitHub. | Enable it in the repository's **Actions** tab. |
| **"Ref '…' was not found in …"** | The branch or tag does not exist. | Pick an existing branch or tag. |
| **"GitHub rejected the request as invalid (check the workflow, ref and inputs)."** | GitHub refused the trigger, for example a missing required input or the workflow is not on that branch. | Check the inputs and that the workflow exists on the branch. |
| **"You don't have permission to create GitHub Action runs in this workspace."** or **"You do not have permission to dispatch workflows (github-actions.dispatch)."** | You lack the start-run permission. | Ask an administrator for `github-actions.dispatch` and create access to runs. |
| **"GitHub could not find the requested repository, workflow, ref or run, or the scope's token has no access to it."** | The item is gone, or the token cannot see it. | Check the repository and branch, and that the token covers the repository. |
| **"The selected scope does not exist or its credential cannot be read."** | The scope was removed or its credential is broken. | An administrator fixes the GitHub scope. |
| **"Invalid workflow inputs: …"** | One or more inputs failed a check, for example a required input is empty, a value is not one of the choices, or a value spans several lines. The message names each input. | Fix the named inputs. Inputs must be a single line. |
| **"A run's spec and scope cannot be changed after it is created. Create a new run instead."** | Runs cannot be edited. | Create a new run. |
| **"workflow_dispatch outcome unknown (HTTP …). It may have started: check GitHub before creating a new run."** | GitHub did not confirm the dispatch. | Check the repository's **Actions** tab before trying again, so the workflow does not run twice. |
| **"The workflow was dispatched but its run could not be identified uniquely (concurrent dispatches). …"** | Several runs of the workflow started at once, so DuploCloud could not tell which was its own. Mostly seen on older GitHub Enterprise Server. | Check GitHub. To make matching exact, add a `duplo_correlation_id` input and a `run-name` that uses it to the workflow. |
| **"You requested this run; another approver must approve it."** (or **"…approve its deployment gates."**) | Four eyes: you cannot approve your own run. | Ask another approver. |
| **"'…' has moved since this run was requested (… → …). Reject this run and create a new one so the new commit is reviewed."** | Someone pushed to the branch after the request. | Reject the run and request a new one. |
| **"Run … started on …, not the approved …; it was cancelled."** | GitHub started the approved run on a different commit, so the agent cancelled it. | Create a new run. |
| **"This run has no recorded requester, so a second approver cannot be proven. Reject it and create a new run."** | Four eyes cannot be checked. | Reject the run and create a new one. |
| **"Ref '…' no longer exists in …. Reject this run."** | The branch was deleted. | Reject the run. |
| **"This run is not awaiting approval."** | Someone already decided. | Refresh the run. |
| **"No environments are awaiting approval for this run."** | The gate was already reviewed, or the run moved on. | Select **Check again** on the Approvals tab. |
| **"This run has no triggered GitHub run yet."** | The run has not been sent to GitHub, so there are no logs. | Wait, or open **View provisioning ticket** to see what the agent is doing. |
| **"GitHub rate limit reached for the scope's token. Try again shortly."** | Too many GitHub calls on that token. | Wait a few minutes. |
| **"GitHub did not respond in time. Try again."** | GitHub was slow or unreachable. | Retry. |
| **"Something went wrong (…). Ref: …"** | An unexpected error. The text in brackets is the error type. | Retry. If it persists, send the reference to your DuploCloud administrator. |
| **"Could not open an AI session."** or **"No AI agent is available in this workspace."** | **Debug with AI** could not start a chat. | Check that the workspace has an AI agent and that you can create helpdesk tickets. |

Errors that come from GitHub end with **Ref: …**. Quote it when you ask for help.

## Other problems

| What you see | What to do |
| --- | --- |
| A button is greyed out | Hover over it to see which permission is missing, and ask an administrator. |
| A run stays at **Ticket Created** | The agent that sends the run to GitHub has not run. Open **View provisioning ticket**. If the ticket shows an authentication error from the AI model, the portal's AI provider credentials need renewing by the platform team. |
| Only step status, no log text | You do not have log permission, or the job has not finished yet. |
| **Debug with AI** did not read the logs | You do not have log permission, so the AI had only the summary. |
| A gate says the scope's token is not a required reviewer | In GitHub, add the token's account as a required reviewer of that environment. |
| No **Required reviewers** option in GitHub | The repository is private and the plan is not GitHub Enterprise. Use protected-branch approval instead. |
| The run never pauses at the gate | The environment has no required reviewers, so GitHub does not hold the run. |
| "Live status unavailable: … Showing the last known values." | DuploCloud could not read the run from GitHub. The reason follows the colon: GitHub unreachable, a token problem, or no access to the run's GitHub scope. Fix the reason given; for scope access, ask an administrator. |
| A run on a protected branch started without approval | Only GitHub branch protection holds a run. Branches covered only by repository rulesets, and tags, start straight away. |
| A branch outside the allow-list still shows, or one you expect is missing | Allow-list patterns are not anchored and ignore case. Use `^branch$` for an exact match. |
| Metrics say some runs may be out of date | The page refreshes up to 25 runs per visit. Open it again. |

## FAQ

**Who appears in GitHub as the person who started or approved the run?** The GitHub account behind the scope's token. DuploCloud records the actual user.

**Does deleting a run delete it in GitHub?** No. Only the DuploCloud record is removed.

**Can I cancel or re-run a run?** Not from DuploCloud. Use GitHub.

**Can I approve my own run?** No, not even as an administrator.

**Does it work with GitHub Enterprise Server?** Yes, when the scope's Account ID is the server's host name.

**Which workflows can I start?** Only those that declare `on: workflow_dispatch`, on repositories and branches the scope allows.
