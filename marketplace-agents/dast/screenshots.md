# Screenshots needed: DAST

Draft by Raman and Claude from the extension repo (UI component text and README). Owner (Arun Hundaragi): please correct and complete this list, and verify each step in QA (https://ai-helpdeskv2-qa01.ai-qa-automation-apps.duplocloud.net/, workspace `agents-qa`). Use test data only: scan a deliberately vulnerable demo application you deploy yourself (for example OWASP Juice Shop in QA), never a customer system. No real account IDs, tokens or customer data; blur URLs and credentials.

| ID | Doc page | Menu path or URL | Setup steps and test data | What to show or highlight | Role |
| --- | --- | --- | --- | --- | --- |
| DA-01 | Set Up | Agent Marketplace > DAST | none | Agent card and the Activate button | admin |
| DA-02 | Set Up | Left menu > Security > DAST (ZAP) | agent activated | The Security section and the DAST (ZAP) entry | admin |
| DA-03 | Set Up | Security > DAST (ZAP) > Add DAST Target, Target step | none | Name, Application URL (demo app), scan type radios with the hint, Max duration, include and exclude paths | admin |
| DA-04 | Set Up / Permissions and Safety | Same step | choose Full (active) | The warning "A full scan sends attack payloads..." | admin |
| DA-05 | Set Up | Add DAST Target, Authentication step | an "other" scope with a test login for the demo app | "Scan as a signed-in user" checked and the scope picker | admin |
| DA-06 | Set Up | Add DAST Target, Source code and Review steps | GitHub scope with a fork of the demo app | Repository multi-select, architecture skills picker, then the Review summary and Create | admin |
| DA-07 | Use | Target page > Run scan | saved target | Run scan window: scan name, scan types, API disabled without a definition URL | admin |
| DA-08 | Use | Run scan window | choose Full | The warning inside the window | admin |
| DA-09 | Use | Scan page, running | start a Baseline scan | Stage list (Queued, Scanning, Triaging...) and the status text | admin |
| DA-10 | Use | Scan page > Artifacts tab | during and after the scan | Live ZAP log, then the HTML report | admin |
| DA-11 | Use | Scan page > Findings tab | completed scan | Stat cards, severity pills, triage filter, rows with Severity, Triage, Source in code | admin |
| DA-12 | Use | Finding details window | click a finding | Evidence, solution, triage reason, severity rationale, Fix this issue button | admin |
| DA-13 | Use | Fix window and Pull requests tab | select two findings, Raise fix PR on the demo fork | Fix window (branch, instructions), then the Pull requests tab with the PR link | admin |
| DA-14 | Permissions and Safety | Target list and target page | read-only test user | What is visible and what is disabled or refused: Add DAST Target, Run scan, Edit, Delete | read-only |
| DA-15 | Permissions and Safety | Scan page, Findings tab | read-only test user | Findings and reports visible; Fix actions disabled or refused, with the message | read-only |
| DA-16 | Permissions and Safety | Target page | regular user with create and update but not `dast.fix` | Run scan works; Fix is refused with the message | regular |
| DA-17 | Permissions and Safety | Admin > permission sets, Fix DAST findings via pull request | admin test user | The named action and its description in the permission editor | admin |
| DA-18 | Use | Target page > Scans tab and Configuration tab | after two scans | Latest scan card, severity bar, scan history, cached architecture brief line | admin |
| DA-19 | Troubleshooting | Scan page failed | scan with an unusable login scope (missing password) | Failed status and the message naming the keys found | admin |
