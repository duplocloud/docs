---
description: Step-by-step walkthroughs of the main things GitHub CI/CD Workflows does.
---

# Use

## Trigger a workflow run

1. Open **CI/CD > GitHub Actions** and select **Trigger Run**.
2. On step **1. Repository & Workflow**:
   - Enter a **Name** for this run record: 2 to 60 letters, numbers or hyphens, starting and ending with a letter or number.
   - Choose the **GitHub Scope**. The **Repository** list loads from it.
   - Choose the **Repository**. The **Workflow** list loads from it.
   - Choose the **Workflow** and select **Next**.
3. On step **2. Branch & Parameters**:
   - Choose the **Branch / Ref**. It starts as the repository's default branch. You can also type a branch or tag name.
   - Fill in the workflow's inputs. Required inputs are marked with an asterisk, and defaults from the workflow are pre-filled.
4. Select **Trigger Run**.

If the workflow does not declare `on: workflow_dispatch`, the form shows a warning and **Trigger Run** stays disabled. If it takes no inputs, the form says so.

{% hint style="info" %}
There is no confirmation step after **Trigger Run**. The workflow starts as soon as you select it.
{% endhint %}

<!-- VERIFY: field labels against the live form (screenshots GH-04 to GH-07). -->

After you trigger the run, DuploCloud starts it on GitHub and records the run number and link. The run record shows **Complete** once GitHub has accepted the trigger. That does not mean the workflow finished. Its own result is shown separately.

<!-- VERIFY: record status wording. "Complete" is the code's value for "trigger accepted". If GitHub shows the run only after a delay, the run number can be empty for a short time; the code allows about 60 seconds to find it. -->

## See your runs

The list shows each run with its **Name**, **Repository**, **Workflow**, **Run** number (a link to GitHub), **Run Status** and the record **Status**. From the row menu choose **View**, **Open in GitHub** or **Track Provisioning**.

## Follow a run

Open a run to see three panels:

- **Spec**: the repository, workflow, branch and the input values you used.
- **Run**: the run number, status, conclusion, branch, trigger time and last refresh, with a link to the run on GitHub.
- **Logs**: each job and its steps with a status icon. Select a step to open its output. The panel refreshes about every 4 seconds while the run is in progress, and **Refresh** reloads it on demand.

GitHub publishes a step's log text only after its job finishes, so a running step shows "log appears once the job finishes". Step status still updates live. Very long logs are cut to the last 200,000 characters.

<!-- VERIFY: panel names and refresh behaviour against the live UI (screenshots GH-08 to GH-10). -->

## Approve or reject a deployment

When a run is waiting for a protected environment, the **Logs** panel shows a banner naming the environment or environments.

1. Optionally enter a comment.
2. Select **Approve** or **Reject**.

All environments currently waiting for that run are approved or rejected together. If GitHub says the token's user cannot approve, both buttons are disabled and the banner says "You are not a required reviewer."

{% hint style="warning" %}
Approving here is done as the GitHub account behind the scope's token, not as you. See [Permissions and Safety](permissions-and-safety.md) before you rely on this for separation of duties.
{% endhint %}

<!-- VERIFY: screenshot GH-11. -->

## Remove a run record

Deleting a run record removes only the DuploCloud tracking record. The run and its history stay in GitHub.

<!-- VERIFY: the list and run pages in the code show no Delete action; delete comes from the platform's standard behaviour. Confirm where the Delete action appears in the UI. -->

## Track the trigger

**Track Provisioning** (list) or **Track Provisioning Status** (run page) opens the DuploCloud ticket that started the run, which is where to look if the trigger failed.
