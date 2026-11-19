# Review notes: GitHub CI/CD Workflows drafts (2026-11-19)

Not for the docs repo. Tells Raman and Kalpesh what to check.

## Sources used
- Repo `duplocloud/duploai-extension-pocs`, folder `extensions/github-actions`, branch `main`, HEAD `1a7a448f395e03e5a28ef02256f20df024bc5cdc` (2026-07-23). The extension's own newest commit is `bdd429de66` (2026-07-22, Kalpesh Suryawanshi, "Added Github actions extension"), also on branch `prorata-extensions`. Branches in the repo: `main`, `jenkins-extensions`, `prorata-extensions`.
- Manifest version 0.1.13 (name "GitHub Actions Trigger").
- Files read: `README.md`, `manifest.json`, `backend/GitHubActionRun.cs`, `backend/GitHubActionRunController.cs`, the three frontend components and service, `skills/provision-github-action-run/*`, the view template.
- Scratch clone: `C:\Users\jaira\AppData\Local\Temp\claude\5a500de405a6674d\28b40241-e91d-4446-a3b5-059de9e36d4e\scratchpad\agents\duploai-extension-pocs`.

## The .NET 10 version is not in this repo
No branch or commit mentions a .NET 10 upgrade. The code comments say "net8". Kalpesh's 2026-11-18 upload must be somewhere else (another repo or an unpushed branch). Ask him for the location and re-check the docs against it.

## VERIFY list
1. Free or paid (README).
2. Admin-only vs user (ClickUp 17twvjx4bm1); warning hint and audience.
3. Read-only, regular and admin rows: the extension has no permissions, so all three come from platform behaviour. Test with three users.
4. Self-approval: code allows it (same token for trigger and approve; no DuploCloud user check). GitHub "Prevent self-review" behaviour not tested.
5. Scope access: helper endpoints do not check that the scope belongs to the workspace.
6. Fine-grained token permission names and classic scopes (inferred from the endpoints).
7. GitHub scope fields in the console, marketplace steps, listing name.
8. UI labels and the status wording against a live run.
9. Where Delete appears in the UI.
10. Whether the platform gates the trigger ticket with approval.
11. Limits (500, 500, 100, 200,000 chars, about 60 seconds).
12. FAQ and error text.

## Not covered
- Screenshots (see `screenshots.md`).
- The sub-tickets from the 2026-11-16 review: self-approval fix, read-only UX, approver notifications, run details UX, new-user value, dashboard v2. None exist in this repo (no notifications, no dashboard, no role handling), so the pages describe the current code only.
- No tests exist in the folder. All behaviour is from reading code.
- Cost, quotas, audit log content.

## For other agents
- This is a proof-of-concept repo: no permission verbs, no `[AccessControl]`, no approval gate. Expect a Permissions page that is mostly VERIFY.
- Real inconsistencies: a code comment says the skill uses the `gh` CLI while the skill and README say `curl`; the README says "approve any pending environment gates" with no DuploCloud-side control; the code calls the extension "GitHub Actions Trigger" and the menu says "CI/CD > GitHub Actions".
- `gh` is not on the Git Bash PATH here; use WSL for API calls. A shallow `git clone` worked fine this time.
- Heredocs with a long body failed in Git Bash; the Write tool is more reliable.
