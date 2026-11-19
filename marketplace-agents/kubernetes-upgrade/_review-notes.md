# Review notes: Kubernetes Upgrader pilot drafts (2026-11-19)

Not for the docs repo. Tells Raman and Bhushan what to check.

## Sources used (scratch clone of duplocloud/duploai-extension-eks-upgrade, version 0.9.15)
- `extensions/eks-upgrade/README.md` (769 lines): almost all content (what it does, safety model, plan and approval, access control, required permissions, recovery, Ask AI data handling, limitations).
- `backend/Permissions.cs`, `EksClusterController.cs`, `EksUpgradeJobController.cs`: action names and the UI permission checks.
- `manifest.json`: menu (Kubernetes Upgrader > Kubernetes Clusters), routes, resources.
- `frontend/src/app/*`: form labels (Add Kubernetes Cluster, Add Upgrade Job, Control Plane Upgrade, Add-on Upgrade, Worker Node Swap, Run pre-flight checks, Create plan).

## Marked VERIFY in the drafts (inferred, not seen running)
1. Free or paid (README overview). Not in the repo.
2. Admin-only decision (Zafar and Bhushan, 2026-11-19; ClickUp DUPLOAI-5602): the menu is still a DevOps menu in the manifest (`DevOpsResource` registrar). The permission tables describe the current permission model and need rewriting to the shipped admin-only behaviour.
3. Read-only and regular user rows: derived from code, not tested with real test users.
4. Marketplace activation steps and the exact menu path after the move.
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
