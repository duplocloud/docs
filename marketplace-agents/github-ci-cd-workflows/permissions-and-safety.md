---
description: What GitHub CI/CD Workflows can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

## What it can read and change

GitHub CI/CD Workflows acts on GitHub with the token of the GitHub scope chosen for the run. It can only do what that token's GitHub account is allowed to do, and only on repositories and branches the scope's allow-lists permit.

| | What it does |
| --- | --- |
| **Reads** | Repositories, branches, tags, branch protection, pull requests and workflow files the token can see; each run's status, jobs, steps, log text and GitHub error annotations. |
| **Changes** | Starts workflow runs (`workflow_dispatch`) with the branch and inputs you choose. Approves or rejects GitHub deployment gates. Cancels an approved run if GitHub started it on a different commit from the one approved. Stores a run record in DuploCloud with the repository, workflow, branch, commit, input values, requester and approval decisions. |
| **Never** | Edits code, workflow files, branches, environments, secrets or settings. Re-runs or deletes runs on GitHub, or cancels them for any other reason. Shows the token to users. Deleting a run in DuploCloud leaves the GitHub run in place. |

{% hint style="warning" %}
Input values are sent to GitHub, stored in the DuploCloud run record and passed to the AI agent that dispatches the run (and to **Debug with AI**). Do not put secrets in workflow inputs. Log text has only GitHub's own secret masking applied, which is why reading it needs a separate permission.
{% endhint %}

## Who can do what

DuploCloud permission sets decide what each person can do. Controls a user cannot use are greyed out with the reason, and the server refuses the same actions if called directly.

| Capability | Read-only user | Regular user | Approver | Administrator |
| --- | :---: | :---: | :---: | :---: |
| See runs, status, step progress, approval history | Yes | Yes | Yes | Yes |
| See the failure summary (without log lines) | Yes | Yes | Yes | Yes |
| See metrics | Yes | Yes | Yes | Yes |
| Read full log text and log lines in the failure summary | No | Yes, with `view-logs` | If also granted `view-logs` | Yes |
| Start a run on an unprotected branch | No | Yes | No (unless also granted `dispatch`) | Yes |
| Request a run on a protected branch | No | Yes (held for approval) | No (unless also granted `dispatch`) | Yes (held for approval) |
| Approve or reject a held run | No | No | Yes, except runs they requested | Yes, except runs they requested |
| Withdraw (reject) their own held run | No | No (needs `approve-run`; ask an approver to reject it) | Yes | Yes |
| Approve a GitHub deployment gate | No | No | Yes, except runs they requested | Yes, except runs they requested |
| Reject a GitHub deployment gate | No | No | Yes | Yes |
| Delete a run record (DuploCloud only) | No | Only if granted delete on runs | No | Yes |
| See and use **GitHub Actions Settings** | No | No | No | Yes |

What each role is made of:

- **Read-only user:** read (GET) access to the workspace's GitHub Action runs, and access to the GitHub scope. Without the scope, the run list still loads, but live status, step progress and the failure summary are unavailable.
- **Regular user:** read and create (GET, POST) on GitHub Action runs, the `github-actions.dispatch` action, access to the GitHub scope, and usually `github-actions.view-logs`.
- **Approver:** added on the **GitHub Actions Settings** page. That grants read access to runs, `github-actions.approve-run`, `github-actions.approve-deployment` and use of the workspace's scopes, nothing else. If you grant `approve-run` through another permission set instead, include access to the GitHub scope too, or the approver can reject runs but not approve them.
- **Administrator:** a DuploCloud administrator. Administrators bypass fine-grained permission checks, with one exception: the four-eyes rule below.

{% hint style="info" %}
**Debug with AI** opens an AI helpdesk chat, which follows your normal helpdesk ticket permissions. GitHub access is attached to the chat only for users with `view-logs`, so the AI cannot read logs the user is not allowed to read.
{% endhint %}

## Four eyes

Nobody can approve a run they requested, **administrators included**:

- A run held on a protected branch can only be approved by someone other than the requester. A requester who is also an approver can withdraw (reject) it.
- A GitHub deployment gate on a run can only be approved by someone other than the requester. The requester can reject it.
- A run with no recorded requester cannot be approved from DuploCloud. Reject it and create a new run, or review the gate in GitHub.

DuploCloud enforces this itself because GitHub sees every action from DuploCloud as the same token account, so GitHub's own **Prevent self-review** cannot tell users apart.

## What needs approval

| Action | Approval |
| --- | --- |
| Start a run on an **unprotected** branch | None. The run starts when a user with permission selects **Trigger Run** and confirms. |
| Start a run on a **protected** branch | Held in DuploCloud until a different user with `approve-run` approves it. Approval dispatches exactly the requested commit; if the branch moved, approval is refused. |
| Pass a GitHub **deployment gate** | A different user with `approve-deployment` approves it in DuploCloud, or a required reviewer approves it in GitHub. |

## Safety checks

- **Scope checks.** A user can only use a scope that is attached to the workspace and that they are allowed to use. Runs always use their stored scope, never one supplied later.
- **Allow-lists.** The scope's repository and branch allow-lists are applied in the pickers and again when a run is created.
- **Manual-trigger workflows only.** Workflows without `on: workflow_dispatch`, and disabled workflows, are refused.
- **Input limits.** At most 25 inputs (GitHub's limit), each up to 4,096 characters, checked against the workflow's declared inputs.
- **No changes after creation.** A run's repository, workflow, branch, inputs and scope cannot be edited. Create a new run instead.
- **One dispatch per run.** A run is sent to GitHub at most once.
- **Locked-down agent.** The agent that sends the run to GitHub may run only its own two scripts without asking. Known ways of reading the GitHub credential or printing environment variables are refused automatically, and any other command needs a person to approve it in the ticket. This applies to the dispatch ticket, not to **Debug with AI** chats.
- **Token never shown.** The token is read by the platform when needed. It is not shown in the form, the run or the logs. In a **Debug with AI** chat for a user with `view-logs`, the AI has the scope's access and is instructed never to print secrets or tokens.
- **Errors without internals.** Unexpected errors and errors from GitHub end with a reference ID instead of internal details.

## Limits you should know

- A started run cannot be cancelled from DuploCloud. Cancel it in GitHub.
- Only GitHub's branch protection holds a run. Branches covered only by repository rulesets, and tags, start without approval.
- Log text appears only after a job finishes, and very long logs keep the last 200,000 characters.
- The metrics page refreshes up to 25 runs from GitHub per visit; others may be slightly out of date.
- Repository and branch lists are read 100 at a time, up to 2,000.
