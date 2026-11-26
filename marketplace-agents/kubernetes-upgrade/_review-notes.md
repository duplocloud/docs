# Review notes: Kubernetes Upgrader pilot drafts (2026-11-19)

Not for the docs repo. Tells Raman and Bhushan what to check.

## Sources used (scratch clone of duplocloud/duploai-extension-eks-upgrade, version 0.9.15)
- `extensions/eks-upgrade/README.md` (769 lines): almost all content (what it does, safety model, plan and approval, access control, required permissions, recovery, Ask AI data handling, limitations).
- `backend/Permissions.cs`, `EksClusterController.cs`, `EksUpgradeJobController.cs`: action names and the UI permission checks.
- `manifest.json`: menu (Kubernetes Upgrader > Kubernetes Clusters), routes, resources.
- `frontend/src/app/*`: form labels (Add Kubernetes Cluster, Add Upgrade Job, Control Plane Upgrade, Add-on Upgrade, Worker Node Swap, Run pre-flight checks, Create plan).

## Marked VERIFY in the drafts (inferred, not seen running)
1. Free or paid (README overview). Not in the repo.
2. ~~Admin-only decision (DUPLOAI-5602)~~ **Done in 0.9.22 (2026-11-26):** the menu is in AI Admin (manifest `"scope": "admin"`, with a Workspace picker on the cluster list) and every endpoint refuses non-administrators (`ADMIN_ONLY`). README, Permissions and Safety, Set Up, Use and Troubleshooting are rewritten to match.
3. ~~Read-only and regular user rows~~ **Replaced and verified:** non-administrators can't use it at all. The permission matrix in CI (qa01, 2026-11-26) refused read-only, regular and approver test users on all 17 endpoints and let the Administrator through (extension repo `tests/api/results/permission-matrix-qa01-ci-2026-11-26.md`).
4. Marketplace activation button names (the menu path is now AI Admin > Kubernetes Upgrader > Kubernetes Clusters).
5. UI wording of the buttons and banners (README and component text, not a live run).
6. AWS and Kubernetes permission lists: copied from the README. A customer-ready policy or CloudFormation template does not exist in the repo.
7. FAQ is a first guess.

## Not covered by these drafts
- Screenshots (see `screenshots.md`).
- Cost and pricing, Ask AI model details, the platform approval window setting (`Workers:EksUpgradeJob:ApprovalWindowMinutes`).
- The repo README says "not covered by automated tests yet", so behaviour claims come from the developers' own verification.

## What this pilot shows for the other agents
- A README that already documents safety, permissions and recovery makes drafting quick. Agents without one will need more developer input; expect shorter, more VERIFY-heavy drafts.
- Draft pages should stay under the docs repo's five-page layout and use GitBook hints. VERIFY comments are HTML comments (not rendered); strip them before the PR is merged.
- Decide with Amal whether the AWS policy list belongs in Set Up (as drafted) or in a separate reference page; it is long.
