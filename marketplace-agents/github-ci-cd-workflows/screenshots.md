# Screenshots needed: GitHub CI/CD Workflows

Capture in QA: https://ai-helpdeskv2-qa01.ai-qa-automation-apps.duplocloud.net/, workspace `agents-qa`, the GitHub scope and test repository named in the pen-test ticket. Its workflows are Sample Deploy, Failure Demo, Gated Deploy, Long Build and Environment Approval Demo; `main` is protected, `dev` is not. Test data only: hide any token, never show real customer data.

Test users in `agents-qa`: `gha-pentest-readonly@example.test` (read-only), `gha-pentest-regular@example.test` (regular: start runs, read logs), `gha-pentest-admin@example.test` (workspace admin, added as an approver on the Settings page), and a DuploCloud administrator for the Settings page.

| ID | Doc page | Menu path or URL | Setup steps and test data | What to show or highlight | Role |
| --- | --- | --- | --- | --- | --- |
| GH-01 | Set Up | Agent Marketplace > GitHub CI/CD Workflows | none | Agent card and the Activate button | admin |
| GH-02 | Set Up | Menu > CI/CD | agent activated | GitHub Actions, GitHub Actions Metrics and GitHub Actions Settings entries | admin |
| GH-03 | Set Up | Workspace scopes > the QA GitHub scope | existing scope (hide the token) | Provider type, Account ID, repository and branch allow-lists | admin |
| GH-04 | Set Up | CI/CD > GitHub Actions Settings | add `gha-pentest-admin@example.test` | Approvers list, Add box, "Also able to approve" list | admin |
| GH-05 | Use | CI/CD > GitHub Actions > Trigger Run | the QA GitHub scope and test repository, workflow Sample Deploy, branch `dev` | Name, scope, repository, workflow, branch and generated inputs (environment choice, version text, dry_run switch); button reads Trigger Run | regular |
| GH-06 | Use | Trigger Run | same, branch `main` | Protected-branch warning; button reads Request Run | regular |
| GH-07 | Use | CI/CD > GitHub Actions (Cards) | at least one succeeded, one failed (Failure Demo), one waiting run | Row cards, filter chips with counts, search box | regular |
| GH-08 | Use | CI/CD > GitHub Actions (Table) | same runs | Table view and the row menu (View, View provisioning ticket, Delete) | admin |
| GH-09 | Use | Run page > Overview | finished Sample Deploy run on `dev` | Run, Request, Workflow inputs, Jobs and GitHub panels; lifecycle rail | regular |
| GH-10 | Use | Run page > Logs | same run | Jobs as sections, steps with status, one step expanded with its log | regular |
| GH-11 | Use | Run page > Approvals | Sample Deploy requested on `main` by `gha-pentest-regular@example.test` | Waiting for approval, commit, requester; Approve and Reject | approver |
| GH-12 | Permissions and Safety | Run page > Approvals | same held run, viewed by its requester | Approve greyed out with the four-eyes reason | regular |
| GH-13 | Use | Run page > Approvals > Deployment gates | Environment Approval Demo waiting on `staging-approval` (needs required reviewers; repo must be public or GitHub Enterprise) | Gate list, Approve selected, Reject selected, timeline | approver |
| GH-14 | Use | Run page > Overview | Failure Demo with `failure_mode` = `tests` | Failure banner (Test > Integration tests), category, hint, log lines, Debug with AI | regular |
| GH-15 | Use | AI helpdesk chat | select Debug with AI on GH-14's run | Chat started by itself with root cause, evidence, fix | regular |
| GH-16 | Use | CI/CD > GitHub Actions Metrics | the runs above | KPI tiles, Overview tab charts, 7d/30d/90d, CSV | regular |
| GH-17 | Permissions and Safety | CI/CD > GitHub Actions | read-only user | Trigger Run greyed out with tooltip; Delete greyed out | read-only |
| GH-18 | Permissions and Safety | Run page > Logs | read-only user, finished run | Step status only, note that log text needs permission | read-only |
| GH-19 | Permissions and Safety | Menu > CI/CD, and the Settings URL opened directly | regular user | No Settings menu item; lock message on the page | regular |
| GH-20 | Troubleshooting | Trigger Run | branch outside the scope's branch allow-list (if one is set) | "Ref '…' is not allowed by the selected scope." | regular |
| GH-21 | Troubleshooting | Run page > Approvals | approve a held run after pushing a new commit to `main` | "'main' has moved since this run was requested" | approver |
