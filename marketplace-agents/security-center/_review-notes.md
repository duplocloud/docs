# Review notes: Security Center drafts (2026-11-19, redone from dev)

Not for the docs repo. Tells Raman and Darren what to check.

## Commit read
Repo `duplocloud-internal/duploai-extension-security-center`, branch `dev`, commit `ce185ae8911343cd309571828fe57240b59d8f50` (2026-11-18, "Merge pull request #77: README says ignoring a gap is a PUT on the Gap"). Extension `extensions/security-center`, manifest id `com.duplocloud.security-center`, version 0.15.30, agent "Compliance". Read through the GitHub contents API (raw files) and a depth-50 clone for the log. The first draft was from `main` (old "SOC 2 Posture", commit 1fb9dbc) and is replaced.

The recent commits are all in dev history: PR #69 / 31e7167 (permission audit fixes), PR #70 (connections must belong to the workspace), PR #71 / f6f79e7 (agent-drafted CLI must be one aws invocation), PR #74, PR #76 / 4b4bd2c (Execute bound to the approved command), PR #77 (README, ignore is a PUT on the Gap).

## Sources used
- `README.md` (Permissions, Architecture, Pages, Impact analysis, CVEs, Jira), `CLAUDE.md` headings, `manifest.json`.
- Backend: `SecurityCenterAccess.cs`, `PostureRemediationsController.cs`, `Remediation/CommandBinding.cs`, `Accounts/AccountDisableRules.cs`, `Accounts/FixAccessRules.cs`, `Accounts/AwsSdkSecurityApi.cs` (SDK call list), `Accounts/AccountSecurityService.cs`, `Settings/PlatformSettings.cs`, `PostureAssessment.cs` (spec fields), all `[AccessControl]` declarations (grep).
- Skills: `remediate-finding/SKILL.md`, `resolve.sh`, `cli_guard.py`; frontend `add-assessment.component.ts`, `view-remediation.component.ts`.
- Not read in detail: the frontend for gaps, overview, settings, impact; `propose.py`; the monitoring, Slack, Jira and CVE backend; the four skills' scripts other than the above; `frontend/src/app/impact/attack-graph.component.ts` failed to download.

## Items marked VERIFY (counts: README 4, Set Up 8, Use 13, Permissions 10, Troubleshooting 2)
1. Scope: dev is far bigger than the Release 1 listing (monitoring, gaps, CVEs, impact analysis, containment, Jira, Slack). Decide what the marketplace pages cover.
2. Free or paid; customer-facing names (manifest agent "Compliance", compliance page titled "Compliance").
3. AWS permission lists: scan reads rebuilt by hand from skill docs; profile-apply list converted by hand from the AWS SDK calls. No ready-made policy exists.
4. Role rows: derived from the extension's declarations and README suggested sets. The platform access filter is not in this repo, and no test user was run.
5. Admin bypass ("confirmed on a live host") is a README statement about the platform.
6. Pull-request push behaviour wording; score history wording (Darren: trend may change); what the resources created in the customer account are called; Slack and Jira connection steps; UI labels everywhere; AI data handling (model, region, retention).

## Earlier five findings (from main), re-checked against dev ce185ae
1. **No access control in code: FIXED.** `SecurityCenterAccess.cs` L21-43 declares seven named actions; every controller carries `[AccessControl]` (for example `PostureRemediationsController.cs` L37, L96, L180, L244). README "Permissions" describes nodes, verbs and actions. Admin bypass is platform behaviour.
2. **Execute on one click: MOSTLY FIXED.** Execute is its own destructive action (`PostureRemediationsController.cs` L180-183), separate from propose-fix, and needs write access attached first (`GrantWrite` L244). The command is bound by SHA-256: `CommandBinding.cs` L18-34, the controller refuses with 409 when the stored command changed, records `approvedCommandSha256` and the approver's email, and `resolve.sh` L525-531 refuses a command that does not match. STILL TRUE: no confirmation dialog (`view-remediation.component.ts` ~L421-426 calls `execute()` directly), and nothing forces a different person to approve than proposed.
3. **Drafted-command guard was a prefix check: FIXED for drafted commands.** `cli_guard.py` is now an allow-list (only letters, digits and a few punctuation marks outside quotes; `$`, backtick and backslash refused inside double quotes; newlines refused), called at `resolve.sh` L200-201 and re-checked before execution at L519-523. `bash -c "$COMMAND"` is still used (L550). Curated commands are not passed through the guard (written by DuploCloud). The re-check at L521 applies only when `priorResult.drafted` is true.
4. **Direct push to the customer repo vs help text: STILL TRUE as behaviour, text contradiction GONE.** `remediate-finding/SKILL.md` L84-94 still pushes the branch straight to the named repo and forks only on failure. The old form help text ("never pushed directly") has no match in the dev frontend.
5. **Remediation create did not check the workspace: FIXED.** `PostureRemediationsController.Create` now loads the gap and returns 404 unless `gap.OwnerWorkspaceId` equals the route workspace (about L107-109); member gaps of a grouped fix are each checked for propose-fix (L121-129).
Extras from the first draft: the "GRC scope" free-text box is now a GRC provider picker, but its value is still never sent or saved (`add-assessment.component.ts` L215-217, L269: `grcScope` is only bound). The version drift (0.11.0 vs 0.8.0 folders) is FIXED: `assemblyDir` and skill folders are all 0.15.30.

## New risks and notes found on dev
- **The extension now changes customer accounts in more ways**: applying an account profile enables Security Hub, Config, CloudTrail, GuardDuty, Inspector, the IAM password policy, a KMS key, an S3 log bucket, EventBridge rules and SQS queues (`AwsSdkSecurityApi.cs` SDK calls; apply endpoint `AccountSecurityService.cs` ~L216, `apply-profile`, destructive). Containment writes to IAM, EC2, Lambda and EventBridge.
- **Action wildcard pitfall** (README, "The action wildcard makes a GET-only rule not read-only"): a set of GET-only rules that also carry `actions: ["*"]` can propose and run fixes. Observed on a live host. Needs a platform-side fix or a loud doc warning (included in the page).
- **Ticket identity**: scan, fix and impact skills post results as PUT on the resource. README says "not yet confirmed for non-admin flows".
- **Disabling services in AWS** is gated by the platform Administrator role in code (`AccountDisableRules.cs` L18-23), not by a named action.
- **EC2 quarantine** and the `::/0` revoke shape are "not yet verified against a real account" (README, Known limitations).
- **Zafar's rule**: candidates are listed in the Permissions page. Execute, grant-write, apply-profile and contain are already separate destructive actions; open questions are admin-only defaults, a second approver, and a confirmation dialog on Approve and run.

## Not covered by these drafts
- Screenshots (see `screenshots.md`).
- Pricing, the scheduled scan details, the Slack alert thresholds and message content, the monitoring worker internals, the data flow page, and the platform-level policy page beyond one mention.
- Tests: nothing was run; the repo has Python and backend test suites that were not executed.
