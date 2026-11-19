# Review notes: Instance Scheduler drafts (2026-11-19)

Not for the docs repo. Tells Raman and Yash what to check.

## Sources used
- Repo: local clone of duploai-instance-scheduler-extension (read-only), commit `4299c28 2026-11-18 Remove light/dark theme toggle (v1.7.39)`. Only one commit in the clone history.
- `README.md` (about 370 lines; partly stale, see below), `manifest.json`.
- `backend/Ec2ScheduledAction.cs`, `Ec2ScheduledActionController.cs`, `RdsScheduledAction.cs`, `RdsScheduledActionController.cs`, `Ec2ScheduledActionExecutorWorker.cs`, `SimpleCron.cs`.
- `skills/provision-ec2-scheduler` and `provision-rds-scheduler` (SKILL.md and the aws commands in provision.sh, used to derive the IAM action lists).
- Frontend: `add/add-esa`, `list/list-esa`, `view/view-esa`, `rds/add-rds`, `rds/list-rds`, `rds/view-rds` (labels, buttons, notices).

## Findings that change the draft
1. Approval flow IS in the code: non-admin Create/Edit/Delete are held (`Spec.Approved=false`, status Waiting for Approval, no provisioning) until an administrator approves, rejects, approves deletion or rejects deletion. Request and review are on the same list and detail pages; there is no separate AI DevOps / AI Admin split in this repo.
2. The repo README is stale: it says non-admins are view-only and buttons are hidden. The code shows request-style buttons ("Edit (request)", "Submit for Approval").
3. DuploCloud mode is NOT removed: DuploHost/DuploTenantId/DuploToken fields, DuploCloud code paths in both controllers, the background `Ec2ScheduledActionExecutorWorker` and provision.sh modes 1, 4, 5 remain. The EC2 form hides the mode picker for new schedules only.
4. ASG scheduling works in AWS scope mode (EventBridge Scheduler calling the Auto Scaling API), contradicting the Slack hint that ASG claims were removed because they only worked in DuploCloud mode.
5. README says EC2 recurring uses Python Lambda `duplo-ec2-{ID}`; the AWS scope script uses only EventBridge Scheduler plus a role. Lambdas exist for RDS and for the DuploCloud-mode path (shared `duplo-ec2-exec-*`).
6. No `[AccessControl]` or named permission verbs: the SDK predates them. Access is by the Administrator role and a read-only claim, checked by hand.
7. Not provably tokenless. Provisioning runs as a platform agent skill; the repo does not show whether a model is involved. I did not claim "no AI".

## VERIFY list (in the drafts)
- Free or paid (not in repo).
- Final role design: admin-only vs request-and-approve (ClickUp 17twvjx4bm2).
- DuploCloud mode and ASG scope for release 1.
- Marketplace steps, menu location (manifest registrar is DevOps), exact labels.
- IAM lists derived from scripts; iam:PassRole, Describe actions and log-read are inferred; no ready-made policy exists.
- Lambda vs EventBridge-only for EC2 recurring.
- Read-only claim never verified against a real platform token (README admits it); regular-user 403 path verified by code review only.
- Tag rule resolution (fixed list at save time?), restore action in AWS scope mode, Pause/Resume for EC2, EC2 logs availability, deprovision leftovers (snapshots, shared RDS role), daylight saving behaviour, AI data handling, FAQ.
- Two sentences added as general AWS knowledge are flagged in place (disk cost when stopped).

## Not covered
- Screenshots (see `screenshots.md`), pricing, the history callback API details, the Executor worker's internals beyond its purpose, CI and local development.
- No automated backend tests exist (README: no C# test project); only 16 shell tests of helper logic. Behaviour claims come from code reading, not a live run.

## Learned for other agents
- Check the controllers, not the README, for permissions. Look for a hand-rolled Administrator check, a read-only claim, and approval fields in the Spec.
- Grep the setup scripts for `aws <service> <command>` to derive IAM lists when the README has none.
- `Approved`, `PendingDeletion` and `WaitingForApproval` in a spec signal Yash's approval flow.
- A README can describe an older design; compare it to controllers and form templates and list contradictions.
- Avoid the word "token" in file names. Use the Write tool for files with apostrophes in bash heredocs failing.
