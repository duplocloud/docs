# Review notes: DAST drafts (2026-11-19)

Not for the docs repo. Tells Raman and the owner (Arun Hundaragi) what to check.

## Sources used
Scratch clone of duploai-extension-dast, branch `main`, commit `bc41b90 2026-11-18 DUPLOAI-5301: build DAST for hosts on SDK 1.2 and later (#3)`, extension version 0.1.19.
- `extensions/dast/README.md`, `manifest.json` (menu Security > DAST (ZAP), 60 min provision timeout).
- `backend/DastTarget.cs`, `DastTargetsController.cs`, `DastScan.cs`, `DastScansController.cs`, `GitHub.cs`: validation, access attributes, `dast.fix`.
- `skills/provision-dast-scan/SKILL.md` and scripts (`run-scan.sh`, `zap-plan.py`, `parse-report.py`, `build-results.py`, `commit-push.sh`, `gh-auth.sh`, `redact-stream.py`), `skills/dast-app-architecture/SKILL.md`.
- Frontend components (target wizard, run-scan window, scan page, fix window, artifacts panel) for labels.
- `docs/dast-extension-spec.txt`, `.claude/skills/duplo-extension-dev/reference/18-access-control.md` (permission model).
- Not used: ClickUp, Slack, QA. Nothing was run.

## What is deterministic vs the AI
Deterministic code: spec validation, ZAP plan, running ZAP in Docker, log redaction, report parsing, result assembly, counts, roll-up to the target. AI agent (instruction-driven): architecture brief, triage (false positives, severity), code mapping, fix edits, commit and PR.

## VERIFY list (summary)
1. Free or paid. Not in repo.
2. Ownership / domain verification for active scans: not in the code at all (critical).
3. Kubernetes scope mandatory in agent setup: nothing in the repo.
4. Max duration and advanced cluster option "disabled for v1": Max duration is present and validated 1 to 240; no cluster option exists.
5. Admin-only vs user (ClickUp 17twvjx4bm0); read-only, regular and admin rows were not tested; no permission-based disabled states in the UI; admin override and audit log undocumented; `dast.fix` not flagged destructive.
6. Marketplace activation steps, exact labels, menu name (DAST vs DAST (ZAP)).
7. Where ZAP runs and the source address to allow-list; whether private apps can be scanned.
8. Exact GitHub credential permissions for read, push and PR.
9. Scan duration and the 60 minute ticket timeout versus Max duration up to 240.
10. "Remediation only tested on Juice Shop" wording.
11. AI model, region and retention for data handling.
12. FAQ and error wording.

## Not covered
Cloud IAM (none required by code), pricing, Kubernetes scope, ownership verification flow, ZAP version pinning (uses the `stable` image), screenshots content (see `screenshots.md`). The repo has no automated tests for the extension (only dev-kit shell tests), so behaviour claims come from reading code.

## What would help other agents
- The README is short and says nothing about safety or roles. Permissions must be derived from controller `[AccessControl]` attributes: verbs GET, PUT, POST, DELETE plus named actions (`Action`, `Destructive`). `ALL` does not grant named actions. Parent grants cascade to children.
- Safety behaviour lives in the skill text (AI instructions) and scripts: separate what code enforces from what the agent is told.
- UI warnings are in the Angular templates; grep for `alert-warning` and `text-warning`.
- Stub names differ from menu names; check `manifest.json` for the real menu.
