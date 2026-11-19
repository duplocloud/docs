# Review notes: AWS Cost Intelligence drafts (2026-11-19)

Not for the docs repo. Tells Raman and Sanket Dangi what to check.

## Sources used
- Local read-only clone of the devkit repo, branch `main`, commit `59eae2b` (2026-11-18, "DUPLOAI-5297: build Cost Intelligence for hosts on SDK 1.2 and later (#44)"). Extension at `extensions/cost-intelligence`, manifest version 0.58.7.
- `extensions/cost-intelligence/README.md` (1741 lines), `docs/SETUP.md`, `docs/ROLES.md`, `docs/ACCESS-MODEL.md`, `docs/USER-GUIDE.md`, `docs/RUNNING-COST.md`, `docs/SECURITY-REVIEW.md`, `docs/TESTS.md`.
- `manifest.json` (menu FinOps > Cost Intelligence, two resources), `backend/Controllers/*` and `Ingest/SourceManagement.cs`, `RefreshAccess.cs`, `CostActions.cs`, `CostFeatures.cs`, the worker, and frontend component labels.
- Not read: CloudFormation templates themselves, most dashboard-specific README sections, the proposal doc.

## Marked VERIFY in the drafts
1. Free or paid (not in the repo). Only AWS Cost Explorer request cost is documented.
2. Admin-only vs user: not decided. Owner decides in ClickUp DUPLOAI id 17twvjx4bkz. Today sources, policies, Connect now and dashboard deletion are admin-only in code; the rest follows permission sets.
3. Read-only and regular rows derived from code, not tested in QA.
4. Whether administrator use reaches the platform audit log (only extension logs and per-item history confirmed).
5. Marketplace activation steps and button names (not in the repo).
6. Form and button labels, including "Refresh data" vs "Refresh cost data".
7. IAM permission list (copied from docs/ROLES.md; the Resource Ownership row is abbreviated) and how customers get the CloudFormation templates.
8. Running cost figures (cite sync code 0.56.64, manifest is 0.58.7).
9. Dashboard count ("nine" in README but ten listed).
10. Ask AI credential (billing credential; review recommends a separate role) and AI model, ticket retention.
11. Jira and ClickUp setup detail placement; FAQ is a first guess.

## Not covered
- Per-dashboard how-to (Tag Attribution settings, KPI goals, Resource Ownership tabs, Credits, Extended Support) and the Commitments planner.
- Screenshots (see `screenshots.md`), Jira and ClickUp step-by-step, the design docs.
- Automated tests exist (716 cases) but were not run; claims come from docs and code reading.

## Learned for other agents
- This repo has real customer-style docs (SETUP, ROLES, USER-GUIDE); drafting was mostly condensing. Check `docs/` before the README.
- Permission truth is in small gate classes (`SourceManagement`, `DashboardManagement`, `RefreshAccess`) and `[AccessControl(Action=...)]` named actions, not only attributes.
- The frontend has `ciLocked` disabled-state messages in `shared/access-errors.ts`: use them for read-only screenshots.
- Docs drift: version numbers in docs lag the manifest.
