# Review notes: Standard Observability drafts (2026-11-19)

Not for the docs repo. Tells Raman, Pankaj Akhade and Srikar Naramsetty what to check.

## Sources used
Scratch clone of the standard-observability extension repo, branch `main`, commit `4b847d5 2026-11-11 Reveal the Grafana password, and make Favourites usable (#16)`. Manifest version 0.1.86. PR #17 is not in this clone, so anything it changes is not reflected.
- `extensions/standard-observability/README.md`: modes, what is deployed, teardown, Grafana SSO prerequisite, ledger.
- `manifest.json`: menu (Observability > Standard Observability), timeouts (provision 2700 s, deprovision 900 s).
- `backend/StandardObservabilityStackController.cs` and `StandardObservabilityStack.cs`: actions, defaults, validation, favourites, grafana-scope.
- `frontend/src/app/*`: wizard steps and labels, stack page, list actions, scope registration, dashboards page.
- `skills/provision-standard-observability/` (SKILL.md, references, scripts, values): phases, AWS CLI calls, hard rules, teardown.

## VERIFY list (inferred or unconfirmed)
1. Free or paid: not in the repo.
2. Admin-only vs user: ClickUp 17twvjx4bm3. No `[AccessControl]`, permission verbs or role-based UI states exist in this repo.
3. Read-only and regular user behaviour: written as UNKNOWN; depends on platform defaults. Test in QA.
4. FluxCD and Load Balancer Controller "required" (wizard) vs warn only (README and run).
5. Full IAM action list and iam:PassRole, S3, ACM permissions; no CloudFormation template exists (sub-ticket).
6. Route 53 permissions seen in QA: not called by extension code; likely external-dns or platform.
7. DevOps-mode S3 role name vs standalone `{cluster}-observability-s3`.
8. Kubernetes RBAC for the Kubernetes scope.
9. Marketplace activation steps, menu path, wizard button labels, error wording (not seen running).
10. "Re-run" = Edit and save.
11. Delete removes only the DB record.
12. Teardown confirmation is prompt-level in the skill, not code-enforced.
13. Grafana admin password visible on stack page to anyone who can view it.
14. Grafana is internet-facing; confirm no internal option.
15. AI data handling section is empty by design.
16. Grafana sign-in allow-list setting path.

## Not covered
Pricing, platform permission defaults, wizard simplification (sub-ticket), the FluxCD and LB-controller prerequisite check as shipped, PR #17, collector-only mode for other clusters (roadmap M3), the Helm chart versions, the tests.

## Inconsistencies in the repo
- README says "Not built for standalone: the wizard" but the wizard has a Standalone mode and Region and EKS Cluster pickers.
- Wizard says FluxCD and the Load Balancer Controller are required; README and skill say only FluxCD fails (standalone) and the controller only warns.
- Wizard hint tells users to "turn on external-dns on the Cluster Add-ons step", but that step installs nothing.
- README says "Observability > Monitoring" menu; manifest has a single item.
- README says "no shared admin password in circulation", yet the password is stored in the spec and revealable on the page.
- QA needed Route 53 permissions; no Route 53 calls exist in the extension.
- SKILL says the agent makes no AWS writes by hand, while the script it runs does many.

## Hints for other agents
- Grep for `[AccessControl]`, Permissions classes and `403` early; this repo had none, so Permissions and Safety became mostly VERIFY.
- The skill's references (phases, teardown) are the best source for "what changes"; grep the scripts for `aws <service> <verb>` calls to build the IAM table.
- Check README claims against the frontend; this README was stale in places.
- Use the Write tool for pages; a long shell heredoc failed here.
