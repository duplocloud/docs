# Screenshots needed: AWS Cost Intelligence

Draft by Raman and Claude from the extension repo (UI component names and README). Sanket Dangi: please correct and complete this list on your branch, and verify each step in QA (https://ai-helpdeskv2-qa01.ai-qa-automation-apps.duplocloud.net/, workspace `agents-qa`). Use test data only: no real account IDs, keys or customer data. The repo's own screenshots show masked real data; do not reuse them.

| ID | Doc page | Menu path or URL | Setup steps and test data | What to show or highlight | Role |
| --- | --- | --- | --- | --- | --- |
| CI-01 | Set Up | Agent Marketplace > AWS Cost Intelligence | none | Agent card and the Activate button | admin |
| CI-02 | Set Up | FinOps > Cost Intelligence | agent activated | FinOps section with the Cost Intelligence entry | admin |
| CI-03 | Set Up | AI Admin > Providers > IT > Cloud > Add | test AWS role | Provider Details step with type AWS | admin |
| CI-04 | Set Up | Attach Scope to Workspaces | scope created | Workspace picker and Attach (not Skip) | admin |
| CI-05 | Set Up | FinOps > Cost Intelligence > Add Cost Data Source | attached QA AWS scope | Name, AWS Scope, Home Region, Cost Metric, Accounts covered | admin |
| CI-06 | Set Up | same form, Advanced open | none | Refresh Schedule, Member Account Role, Assume Role ARN | admin |
| CI-07 | Use | Source page > Add dashboard | existing source | Dashboard kind dropdown with all kinds | admin |
| CI-08 | Use | Source page after first sync | source synced | Status Complete, accounts, warnings box, Refresh data and Policies buttons | admin |
| CI-09 | Use | Cost and Usage > Billing Summary | synced source | Tiles, trend, date range and PDF menu | admin |
| CI-10 | Use | Action Center > Open items | Action Center dashboard added | Grouping by status, In work section | admin |
| CI-11 | Use | Action Center item dialog > Create ticket | pick an item | Ticket preview before approval | admin |
| CI-12 | Use | Action Center > Settings | none | Ticket system choice (Helpdesk, ClickUp, Jira) | admin |
| CI-13 | Use | Source page > Policies | none | Policy list with switches, Add policy | admin |
| CI-14 | Permissions and Safety | Source list | read-only test user | Add Cost Data Source disabled with the message | read-only |
| CI-15 | Permissions and Safety | Source page | read-only test user | Refresh data, Edit, Delete disabled with reason on hover | read-only |
| CI-16 | Permissions and Safety | Dashboard header | read-only test user | Ask AI panel showing read-only notice; Settings disabled | read-only |
| CI-17 | Permissions and Safety | Dashboard and Action Center item | regular user with Put and Post but not `finops.sync` | Ask AI and Create ticket work; Refresh data disabled; adding Tag Attribution refused | regular |
| CI-18 | Permissions and Safety | Source page > Policies | regular user | Policies readable, changes disabled (administrator only) | regular |
| CI-19 | Use | Dashboard > Ask AI | open the panel | Chat with a sample question and Previous conversations tab | admin |
| CI-20 | Use | Add dashboard > Custom | prompt entered | Brief with Build, Edit, Back | admin |
| CI-21 | Use | Update Dashboard > Revision history | a few builds | Versions with Revert | admin |
| CI-22 | Permissions and Safety | Ask AI approval request in the ticket | ask a live question | AWS command waiting for approval | admin |
