---
description: What GitHub CI/CD Workflows can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

## What it can read and change

GitHub CI/CD Workflows acts on GitHub with the access token of the GitHub scope you choose. It can do only what that token's GitHub account is allowed to do.

| | What it does |
| --- | --- |
| **Reads** | The repositories the token can see (private ones included), their workflows and branches, the workflow definition file (to build the input form), and each run's status, jobs, steps and log text. |
| **Changes** | It starts workflow runs (GitHub's manual trigger) with the branch and inputs you choose. It approves or rejects deployments that a run is waiting on, with an optional comment. It stores a tracking record in DuploCloud with your repository, workflow, branch and input values. |
| **Never** | It does not edit code, workflow files, branches or settings, and does not re-run, cancel or delete runs on GitHub. Deleting the DuploCloud record leaves the GitHub run in place. |

{% hint style="warning" %}
Input values you enter are sent to GitHub as workflow inputs and are stored in the DuploCloud tracking record. Do not put secrets in workflow inputs.
{% endhint %}

<!-- VERIFY: the "stores input values" statement comes from the spec saved on the run record. Confirm retention and whether the platform masks them. -->

## Who can do what

This extension defines **no permission names of its own**. It has no approve, trigger or read-only permission, and no administrator override in its code. Access to the run list, the create form and the run page comes from the DuploCloud platform's standard handling of workspace resources.

| User | What the code shows |
| --- | --- |
| **Read-only** | Not defined by this extension. The list shows a **Trigger Run** button and the run page shows **Approve** and **Reject** whenever a run is waiting, with no read-only state in the page. Whether the platform blocks a read-only user from creating a run is not visible in this repo. |
| **Regular user** | Anyone the platform lets create resources in the workspace can trigger a run with any GitHub scope attached to that workspace. |
| **Administrator** | No separate behaviour in this extension. |

<!-- VERIFY: all three rows. The repo has no [AccessControl] attributes, no permission verbs, no administrator override and no disabled states for read-only users. What a read-only or regular user can do comes from the inherited platform controller and must be tested in QA with a read-only, a regular and an admin test user (screenshots GH-12 to GH-15). -->
<!-- VERIFY: the owner decides whether this agent is admin-only or open to users (ClickUp 17twvjx4bm1). The review of 2026-11-16 raised sub-tickets on a self-approval fix, a read-only experience, approver notifications, run details, value for new users and a second dashboard. None of these exist in the repo today. Rewrite this table to the shipped design. -->

### Which GitHub scopes a person can use

The create form lists scopes attached to the workspace. The repository, workflow, branch and input lists are read with the scope you pick.

<!-- VERIFY: the helper lists (repos, workflows, branches, workflow inputs) take a scope ID from the request and do not check that the scope belongs to the current workspace. Only the per-run pages (logs, approve) check that the run belongs to the workspace. Confirm with the owner whether the platform enforces scope access before these calls. -->

## What needs approval

- **Triggering a run: no approval in DuploCloud.** There is no confirmation step and no second person involved. The run starts when the user selects **Trigger Run**.

<!-- VERIFY: the trigger runs as a platform ticket handled by an agent. Confirm whether the platform asks for approval before that agent acts, and whether the ticket shows who triggered it. -->

- **Deployments to protected environments: approved in GitHub's own way.** If your workflow uses a protected environment, GitHub pauses the run until a required reviewer approves. GitHub CI/CD Workflows lets you give that approval from the run page.

### Can the person who triggers a run also approve it?

Read this before you rely on approvals for separation of duties.

- Triggering and approving both use the **same GitHub token**, so both appear in GitHub as the same GitHub account.
- DuploCloud does not check who you are when you approve. Any DuploCloud user who can open the run page can select **Approve**, if the token's GitHub account is a required reviewer for that environment.
- The **Approve** and **Reject** buttons are enabled or disabled by GitHub's answer about the token's account, not about the DuploCloud user.
- GitHub's own **Prevent self-review** setting on an environment, if you turn it on, applies to that one GitHub account, not to the individual DuploCloud users behind it.

So, as built, the person who triggers a run can also approve it. A fix is expected but is not in the code.

<!-- VERIFY: the sub-ticket for the self-approval fix. Confirm the intended behaviour (for example, require a different DuploCloud user, or per-user GitHub credentials) and whether it ships in the first release. Also confirm how GitHub treats approval when the trigger and the approval come from the same token user and "Prevent self-review" is on; this is GitHub behaviour and was not tested. -->

## Safety checks

- **Manual-trigger workflows only.** The form warns and disables **Trigger Run** if the workflow does not declare `on: workflow_dispatch`.
- **GitHub decides.** GitHub rejects a trigger the token is not allowed to make, or a workflow or branch that does not exist, and the error is shown on the record.
- **Credentials stay out of the page.** The token is read by the platform from the scope when needed and is not shown in the form, the run record or the logs view.
- **Read-only calls for status.** Opening a run, its logs or the list only reads from GitHub.

## Limits you should know

- A trigger cannot be undone from DuploCloud. Cancel the run in GitHub if you need to stop it.
- The run's result comes from GitHub when you open the run. If GitHub is unreachable, the last known values are shown.
- Log text for a step appears only after its job finishes, and very long logs are cut to the last 200,000 characters.
- Lists are capped: 500 repositories, 500 branches, the first 100 workflows.
- The extension records the run only when GitHub shows it within about a minute. If not, the run was still triggered, but its number may be missing until the next refresh.

<!-- VERIFY: limits come from code constants (500, 500, 100, 200,000 characters, about 60 seconds). Confirm they are intentional for release. -->
