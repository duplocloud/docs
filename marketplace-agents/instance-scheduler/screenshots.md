# Screenshots needed: Instance Scheduler

Draft by Raman and Claude from the extension repo (UI component source and manifest). Yash Jain: please correct and complete this list, and verify each step in QA (https://ai-helpdeskv2-qa01.ai-qa-automation-apps.duplocloud.net/, workspace `agents-qa`). Use test data only: no real account IDs, tokens or customer data.

| ID | Doc page | Menu path or URL | Setup steps and test data | What to show or highlight | Role |
| --- | --- | --- | --- | --- | --- |
| IS-01 | Set Up | Agent Marketplace > Instance Scheduler | none | Agent card and the Activate button | admin |
| IS-02 | Set Up | Menu > Scheduler | agent activated | Scheduler section with EC2 and RDS entries | admin |
| IS-03 | Set Up / Use | Scheduler > EC2 > Schedule Action | QA AWS scope | Details card: Name and AWS Scope picker | admin |
| IS-04 | Set Up / Use | Scheduler > RDS > Schedule Action | QA AWS scope | Name and AWS Credential Scope fields | admin |
| IS-05 | Use | EC2 form, Target | pick scope; two test instances tagged `env=test` | The three tabs (Auto Scaling Group, Tags, Instance IDs) and an ASG-managed instance shown disabled | admin |
| IS-06 | Use | EC2 form, Action and Schedule | choose Stop, turn on the paired Start | Stop/Start/Reboot cards, paired time, One-time and Recurring toggle | admin |
| IS-07 | Use | EC2 form, Recurring | choose Daily 21:00 or Custom cron | Frequency options and the UTC cron field | admin |
| IS-08 | Use | EC2 form footer | click Dry run | Dry run result card and footer summary | admin |
| IS-09 | Use | EC2 form, Auto Scaling Group tab | test ASG | Min, Max, Desired fields, CA badge, restore option, Execute now toggle | admin |
| IS-10 | Use | RDS form, Target and Action | Load DB Instances; test DB | DB list, state-conflict warning, snapshot toggle, 7-day auto-restart warning | admin |
| IS-11 | Use | RDS form, Schedule | recurring plus paired Start | Cron preview, paired section, maintenance-window warning if shown | admin |
| IS-12 | Permissions and Safety | EC2 and RDS lists | read-only test user | Schedule Action, Edit, Delete greyed out with tooltip | read-only |
| IS-13 | Permissions and Safety | Schedule detail page | read-only test user | No Execute Now, Pause or Approve; view-only content (history, logs, health) | read-only |
| IS-14 | Permissions and Safety | Scheduler > EC2 > Schedule Action | regular (non-admin, non-read-only) test user | "Requires approval" notice and the Submit for Approval button | regular |
| IS-15 | Permissions and Safety | EC2 and RDS lists | regular user submits a request | Row with status Waiting for Approval; menu shows Edit (request), Delete (request) and no Approve | regular |
| IS-16 | Use / Permissions and Safety | Row menu on a pending request | admin test user | Approve and Reject menu items on a Waiting for Approval row | admin |
| IS-17 | Use | Approve and Reject prompts | admin clicks each | Approve confirmation text and Reject reason prompt | admin |
| IS-18 | Use | Row with Pending Deletion | regular user requests a delete of a live schedule | Pending Deletion badge, Approve Deletion and Reject Deletion items (admin view) | admin |
| IS-19 | Permissions and Safety | Request rejected | admin rejects with a reason | Status Failed and the rejection reason on the detail page | admin |
| IS-20 | Use | RDS detail page | recurring RDS schedule with history | Execute Now or Pause/Resume buttons (admin), execution history, snapshots table, logs | admin |
| IS-21 | Use | EC2 detail page | live EC2 schedule | Live state, Last Executed, History and Logs tabs | admin |
| IS-22 | Troubleshooting | Form with a past one-time date | enter a past date | The "in the past" error | admin |
