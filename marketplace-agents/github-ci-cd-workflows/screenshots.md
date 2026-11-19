# Screenshots needed: GitHub CI/CD Workflows

Draft by Raman and Claude from the extension repo (UI component text and README). Kalpesh: please correct and complete this list on your branch, and verify each step in QA (https://ai-helpdeskv2-qa01.ai-qa-automation-apps.duplocloud.net/, workspace `agents-qa`). Use a test repository and test data only: no real tokens, org names or customer data.

| ID | Doc page | Menu path or URL | Setup steps and test data | What to show or highlight | Role |
| --- | --- | --- | --- | --- | --- |
| GH-01 | Set Up | Agent Marketplace > GitHub CI/CD Workflows | none | Agent card and the Activate button | admin |
| GH-02 | Set Up | Menu > CI/CD > GitHub Actions | agent activated | The CI/CD section and the GitHub Actions entry | admin |
| GH-03 | Set Up | Workspace scopes (GitHub source-control scope) | test GitHub scope with a throwaway fine-grained token (hide the token) | Provider type and Account ID fields | admin |
| GH-04 | Use | CI/CD > GitHub Actions > Trigger Run, step 1 | test scope, test repo with a manual-trigger workflow | Name, GitHub Scope, Repository and Workflow pickers | admin |
| GH-05 | Use | Trigger Run, step 2 | pick a workflow with a choice, a boolean and a text input | Branch / Ref and the generated input fields | admin |
| GH-06 | Use | Trigger Run, step 2 | pick a workflow without `workflow_dispatch` | Warning and disabled Trigger Run | admin |
| GH-07 | Use | CI/CD > GitHub Actions (list) | trigger two runs | List with Run, Run Status and Status columns and the row menu | admin |
| GH-08 | Use | Run page > Run panel | open a finished run | Run number, status, conclusion and GitHub link | admin |
| GH-09 | Use | Run page > Logs panel | a running multi-step workflow | Jobs and steps with live status | admin |
| GH-10 | Use | Run page > Logs panel | expand one finished step | Step log output | admin |
| GH-11 | Use / Permissions and Safety | Run page > Logs panel | test repo with a protected environment, run waiting | Approval banner, comment box, Approve and Reject | admin |
| GH-12 | Permissions and Safety | CI/CD > GitHub Actions (list) | read-only test user | Whether Trigger Run is shown or disabled | read-only |
| GH-13 | Permissions and Safety | Run page > Logs panel | read-only test user, waiting run | Whether Approve and Reject are enabled | read-only |
| GH-14 | Permissions and Safety | Trigger Run | regular test user | Create works with an attached scope | regular |
| GH-15 | Permissions and Safety | Run page > Logs panel | regular user, token account is the reviewer | Approve enabled for the same person who triggered (self-approval) | regular |
| GH-16 | Troubleshooting | Trigger Run, step 1 | scope without a usable token | Error under the Repository field | admin |
| GH-17 | Troubleshooting | Run page > Logs panel | token user not a required reviewer | "You are not a required reviewer." with disabled buttons | admin |
