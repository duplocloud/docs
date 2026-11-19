# Screenshots needed: SRE

Draft by Raman and Claude from the extension repo (UI component names and README). Pallavi: please correct and complete this list on your branch, and verify each step in QA (https://ai-helpdeskv2-qa01.ai-qa-automation-apps.duplocloud.net/, workspace `agents-qa`). Use test data only: no real account IDs, tokens or customer data. Use a synthetic alert such as an Alertmanager body with alertname `TestHighErrorRate`, severity `warning`, service `demo-service`.

| ID | Doc page | Menu path or URL | Setup steps and test data | What to show or highlight | Role |
| --- | --- | --- | --- | --- | --- |
| SR-01 | Set Up | Agent Marketplace > SRE | none | Agent card and the Activate button | admin |
| SR-02 | Set Up | Observability > SRE | agent activated | SRE entry in the menu; empty state "No alert hub yet" | admin |
| SR-03 | Set Up | SRE > Create your first alert hub > Basics | none | Hub name and "Alerts come from" | admin |
| SR-04 | Set Up | New alert hub > Investigations | QA test scopes (observability, optional Kubernetes) | Access pickers and the Read-only, Custom, Full access presets | admin |
| SR-05 | Set Up | New alert hub > Remediation | same | "Same access as investigations" and the Custom rules default | admin |
| SR-06 | Set Up | New alert hub > Advanced options (Skills, Runbooks, Notifications) | optional | Runbooks source choices and the Slack notification scope | admin |
| SR-07 | Set Up | Hub created page | create a test hub | Webhook URL, Copy and Send a test alert | admin |
| SR-08 | Use | Hub > Alerts | ingest the test alert | Alerts list with filters, selection, Reason, Skip, Investigate | admin |
| SR-09 | Use | Hub > Alerts > Ingest Alert | paste the synthetic body | Ingest form and the "What happens" notes | admin |
| SR-10 | Use | Hub > Alerts > an alert | open the test alert | Alert details, occurrence count, labels, history | admin |
| SR-11 | Use | Hub > Investigations > an investigation (running) | investigate the test alert | Execution pipeline and status | admin |
| SR-12 | Use | Investigation > RCA (complete) | wait for the run | Problem, root cause, findings, evidence inspector, Runbooks card | admin |
| SR-13 | Use | Investigation > Actions | complete investigation with actions | Recommended actions, Execute in Ticket, Details | admin |
| SR-14 | Use | Investigation > Edit RCA | click Edit RCA | Editor and the version picker after saving | admin |
| SR-15 | Use | Hub > Rules | add a rule `severity` equals `warning` | Rule form and Dry run results | admin |
| SR-16 | Use | Investigation > Split Investigation | an investigation with two root causes (if available) | Split preview: moving vs staying | admin |
| SR-17 | Use | Investigation > Runbook | click Draft Runbook | Runbook tab with draft and Create Runbook | admin |
| SR-18 | Permissions and Safety | Hub > Investigations > an investigation | read-only test user | View works; try Edit RCA or Execute and capture the permission message | read-only |
| SR-19 | Permissions and Safety | Hub > Alerts | read-only test user | Investigate and Skip outcome (disabled or error) | read-only |
| SR-20 | Permissions and Safety | Hub > Alerts and an investigation | regular user with investigate and skip but not execute-action | Investigate works, Execute in Ticket refused with the message | regular |
| SR-21 | Permissions and Safety | Permission-set editor | admin | The SRE node and the named actions, with the destructive flags | admin |
| SR-22 | Permissions and Safety | Hub settings > Investigations > Permissions | open the page | Presets and the Rules in use for Read-only | admin |
| SR-23 | Permissions and Safety | Investigation > View Ticket | use a Custom preset that asks | Approval prompt for a command | admin |
| SR-24 | Use | Slack channel | Slack test scope set on the hub | Investigation thread with root cause and findings | admin |
