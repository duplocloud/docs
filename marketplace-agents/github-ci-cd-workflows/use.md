---
description: Step-by-step walkthroughs of the main things GitHub CI/CD Workflows does.
---

# Use

## Start a run

1. Open **CI/CD > GitHub Actions** and select **Trigger Run**.
2. Fill in the form:
   - **Name**: 2 to 60 letters, numbers or hyphens, starting and ending with a letter or number. For example `deploy-staging`.
   - **GitHub Scope**: the scope whose token runs the workflow.
   - **Repository**: only repositories the scope allows are listed.
   - **Workflow**: the repository's workflows.
   - **Branch / Ref**: pick or type a branch or tag, or pick a pull request to run its branch.
3. Fill in the workflow's inputs. Each input the workflow declares is shown with its type, default and whether it is required: a choice is a dropdown, a boolean a switch, anything else a text box.
4. Select the button at the bottom.

The form checks the branch as you pick it:

- **Unprotected branch:** the button reads **Trigger Run**. The workflow starts as soon as you select it.
- **Protected branch:** the form warns you and the button reads **Request Run**. Nothing is sent to GitHub until an approver releases the run.

If the workflow does not declare `on: workflow_dispatch`, it cannot be started. If you do not have permission to start runs, the form and the button are greyed out and say why.

## Find a run

**CI/CD > GitHub Actions** lists the workspace's runs, newest first.

- **Cards** (default): each run is a full-width row with a coloured edge and icon for its state, the name and workflow, repository and branch, run number and duration, who requested it and when, the approval state and a status badge. Select a row to open the run.
- **Table**: a classic table. Switch with **Cards | Table**. Your choice is remembered in this browser.
- **Search** by run name, repository, branch, workflow, requester or status.
- **Filter chips**: **All**, **In progress**, **Needs approval**, **Failed**, **Succeeded**, each with a count.
- **Row actions**: the GitHub icon opens the run in GitHub. The menu has **View**, **View provisioning ticket** and **Delete**.

The list shows 24 runs at a time. Runs still in progress refresh from GitHub when you open the list.

## Follow a run

Open a run to see its header, three tabs and a lifecycle rail.

- **Header:** name, live status, who requested it and when, and **Open in GitHub**.
- **Overview tab:** anything the run is waiting on comes first (an approval or a deployment gate). A failed run shows its failure summary next. Then panels for **Run** (run number, status, duration, commit, with GitHub links), **Request** (workflow file, requested commit, requester, scope, whether approval was needed), **Workflow inputs**, **Jobs**, and **GitHub** (an **Open in GitHub** button).
- **Logs tab:** each job is a section and each step a row with its status. The tab updates by itself while the run is in progress, and **Refresh** updates it now. Users with log permission can open a step to read its log. Others see step status and a note. A failed step opens by itself.
- **Approvals tab:** the protected-branch approval, GitHub deployment gates, and a timeline of every decision.
- **Lifecycle rail:** **Requested > Approval > Dispatched > Running > Succeeded / Failed**, with the current stage highlighted.

GitHub publishes a job's log text only when the job finishes. Very long logs are cut to the last 200,000 characters.

**View provisioning ticket**, under every tab, opens the helpdesk ticket that sent the run to GitHub. Use it to see what the agent did.

## Approve a run on a protected branch

A run requested on a protected branch shows **Waiting for approval**.

1. Open the run. It opens on the **Approvals** tab.
2. Check what will run: workflow, repository, branch, the exact commit and who requested it.
3. Optionally add a comment, select **Approve** or **Reject**, and type the run name to confirm.

- Approval runs exactly the requested commit. If someone pushed to the branch since, approval is refused. Reject the run and request a new one.
- If you requested the run, **Approve** is greyed out. If you are an approver, **Reject** reads **Withdraw**, so you can cancel your own request. A requester who is not an approver asks an approver to reject it.
- The Approvals tab records who decided, when, how long it waited, the approved commit and the comment.

## Review GitHub deployment gates

When a run waits on a GitHub environment gate, the Overview tab says so and the Approvals tab is marked.

1. On the **Approvals** tab, under **Deployment gates**, tick the environments to review.
2. Optionally add a comment and select **Approve selected** or **Reject selected**, then confirm.
3. **Check again** reloads the gate list.

The person who requested the run can reject its gates but not approve them. Reviews made directly in GitHub also appear in the timeline, with the channel **GitHub**.

## When a run fails

The Overview tab starts with a failure banner, for example "Failed at Test > Integration tests: tests failed." It shows the job and step, a cause category (missing secret or input, authentication or permission, network, timeout, dependency install, tests failed, cancelled, or exit code), a hint, and up to 10 log lines around the error if you have log permission.

**Debug with AI** opens an AI helpdesk chat that starts by itself. The AI gets the repository, branch, commit, workflow, inputs, failed step and summary. If you have log permission it also gets access to the run's GitHub scope, reads the failed job's log, the workflow file and the last successful run, and reports the root cause, the evidence, a fix and whether it is safe to re-run. Without log permission it works from the summary only. The AI is told not to re-run, dispatch, approve or change anything.

## Metrics

**CI/CD > GitHub Actions Metrics** (or **View metrics** on the run list). Pick **7d**, **30d** or **90d**. **CSV** downloads the daily numbers.

- **KPI tiles:** runs requested, success rate, failure rate, median run time, lead time (request to finish) and approval wait, each with a daily trend and the change against the previous period.
- **Overview:** runs per day by outcome, an outcome donut, the success-rate trend, a weekday-by-hour heatmap, and top failure causes.
- **Reliability:** workflows failing right now, time to recover, dispatch reliability.
- **Approvals:** held, approved and waiting counts, approval-wait distribution, top approvers and requesters.
- **Repositories & workflows:** runs, failures, success rate and run time per repository, and the most-run workflows.
- **Run time:** total, median, 90th percentile and lead time, minutes per day, and spread per workflow.
- **Anomalies:** failure spikes, often-failing repositories, unusually slow runs, approvals waiting over a day, failing dispatches.

Days and hours are UTC. Run time is wall-clock time, not GitHub billed minutes.

## Delete a run record

**Delete** removes only the DuploCloud record. You confirm by typing the run name. The run, its logs and artifacts stay in GitHub.
