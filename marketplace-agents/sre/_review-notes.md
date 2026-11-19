# Review notes: SRE drafts (2026-11-19)

Not for the docs repo. Tells Raman and Pallavi what to check.

## Sources used
- Repo: duploai-extensions-sre (local read-only clone), `extensions/sreworkbench`, branch `main`, commit `467c458` (2026-11-18, "Merge pull request #61 from duplocloud/feat/sreworkbench-status-colors-hide-incident").
- `README.md` (safety/permissions/notifications/runbooks), `manifest.json` (version 0.17.6, menu Observability > SRE), `backend/*Controller.cs` ([AccessControl] declarations), `AlertFingerprint.cs`, `AlertIngestionService.cs`, `CommandPermissionPolicy.cs`, `RemediationPhase.cs`, `AlertHub.cs`, `AutoInvestigationRule.cs`, `InvestigationStage.cs`, `skills/duploaisre/SKILL.md` and `native-mode.md`, `skills/runbookscan/SKILL.md`, `frontend/src/app/*` (labels), `docs/slack-configuration.md`, `docs/PRODUCTION-READINESS.md`, `AccessDeclarationTests.cs`. Tests were read, not run.

## VERIFY list (inferred or not confirmable from code)
1. Customer-facing name (SRE / SRE Workbench / AI SRE).
2. Admin-only vs user (owner decision, ClickUp 17twvjx4bm4): README hint, Permissions tables, FAQ.
3. Free or paid; console shows paid with no published version. No price claimed.
4. Alert sources actually tested (Datadog, CloudWatch, PagerDuty are labels only).
5. Marketplace activation steps and button names.
6. Cloud IAM / Kubernetes roles for scopes: repo lists none; recommended read-only policies?
7. Slack: UI text says "webhook URL"; code and guide use bot token + channel ID.
8. How the external alert source authenticates to the webhook.
9. "Send a test alert" runs a real investigation (cost).
10. Phase names and typical duration in the UI.
11. Read-only/regular rows untested; whether Alerts list buttons are disabled or error on click.
12. Administrator override and audit logging: not in repo.
13. Pre-0.14.0 upgrade note.
14. Default command policy (README says Full; code says Read-only for new UI hubs, Full when no policy).
15. Readiness audit gaps (prompt injection, audit log) still open?
16. Scope credentials visible in the ticket Files panel.
17. Model, provider, retention and region for AI data.
18. OpenSRE mode: dormant per skill file.
19. Error message wording; FAQ list.

## Not covered
- Hub settings pages detail, Skills section, runbook scan ("Scan with the agent"), Overview stat cards.
- Pricing, limits, performance (none stated in repo), the .NET 10 upgrade and QA deployment state.
- Behaviour in a live environment; no screenshots.

## Inconsistencies found in the repo
- README says the extension wraps the OpenSRE CLI and defaults to it; `opensre-mode.md` is marked DORMANT and the hub form creates native-mode hubs.
- README says default command policy is Full access; new UI hubs default to Read-only. README's "Approve All / Reject All" switches are replaced by Ask / Approve / Reject.
- Notifications UI text says webhook URL; backend uses a Slack bot token and channel ID.
- `manifest.json` version is 0.17.6 but `assemblyDir` and skill folders say 0.14.0.
- `docs/PRODUCTION-READINESS.md` (0.11.0) says no `[AccessControl]` exists; it now does. The audit is stale.
- README frontend section says the menu is "SRE > Alert Hubs"; the manifest has Observability > SRE (README local-dev path says Analytics > Observability > SRE).
- Hub overview shows "Mode ... opensre" as fallback when mode is empty; investigation view treats empty as native.

## Helpful for other agents
- Check the `[AccessControl(Action=...)]` attributes and the `AccessDeclarationTests` first: they give the exact permission list.
- The UI source gives real labels, but verify against QA; READMEs lag the code.
- Look for stale audit or readiness docs in `docs/` and do not quote them without checking the current code.
