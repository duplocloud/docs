# Screenshots needed: Standard Observability

Draft by Raman and Claude from the extension repo (wizard and page components, manifest, README). Pankaj Akhade and Srikar Naramsetty: please correct and complete this list, and verify each step in QA (https://ai-helpdeskv2-qa01.ai-qa-automation-apps.duplocloud.net/, workspace `agents-qa`). Use test data only: no real account IDs, passwords, tokens or customer data. Blur the Grafana admin password.

| ID | Doc page | Menu path or URL | Setup steps and test data | What to show or highlight | Role |
| --- | --- | --- | --- | --- | --- |
| SO-01 | Set Up | Agent Marketplace > Standard Observability | none | Agent card and the Activate button | admin |
| SO-02 | Set Up | Observability > Standard Observability (menu) | agent activated | The Observability section and item in the left menu | admin |
| SO-03 | Use | Standard Observability > Create Observability Stack | workspace with no stack | Empty state with the create button | admin |
| SO-04 | Use | Wizard step 1 Basics | QA AWS and Kubernetes scopes | Stack name and the two Provisioning Mode buttons | admin |
| SO-05 | Use | Wizard step 1, standalone | choose Standalone, region, test EKS cluster | Region and EKS Cluster pickers | admin |
| SO-06 | Use | Wizard step 2 Cluster Add-ons | test cluster | Add-on status badges, required labels, Re-check | admin |
| SO-07 | Use | Wizard step 3 Node Pool | none | Create New Node Pool and Use Existing Nodes, sizes | admin |
| SO-08 | Use | Wizard steps 4 and 5 | none | Log Storage (bucket choice, retention) and Monitoring (retention, disk, size cap) | admin |
| SO-09 | Use | Wizard step 6 Grafana | test password (not a real one) | Password rules hint and Portal URL for SSO | admin |
| SO-10 | Use | Wizard steps 7 and 8 | test ACM certificate and DNS zone | Endpoints with DNS mode choice, then Review & Submit with the issue list | admin |
| SO-11 | Use | Stack page while provisioning | submit a small test stack | Phase list with states | admin |
| SO-12 | Set Up | Administrator > System Settings > System Config | add `AppConfig/otel` for the test Grafana host | The setting row (host is a test host) | admin |
| SO-13 | Use / Troubleshooting | Stack page, status Blocked | choose "I will create it" | Action required - create this DNS record with Copy and re-check | admin |
| SO-14 | Use | Stack page, Grafana panel | complete test stack | Register the Grafana scope notice and Create Grafana scope button | admin |
| SO-15 | Use / Permissions and Safety | Stack page, Grafana panel | non-admin user, existing attached scope | Associate an existing scope picker and Save, and the refusal message after a failed create | regular |
| SO-16 | Use | Observability > Standard Observability (dashboards page) | complete stack with monitoring | Stack and dashboard pickers, kiosk toggle, an embedded dashboard | admin |
| SO-17 | Use | List menu > Deprovision | test stack | Teardown summary prompt showing what goes and what stays | admin |
| SO-18 | Permissions and Safety | Stack list | read-only test user | Whatever the platform shows or disables for create, edit, deprovision, delete | read-only |
| SO-19 | Permissions and Safety | Stack page | read-only test user | Stack page, favourites controls, Grafana scope controls | read-only |
| SO-20 | Permissions and Safety | Stack list and wizard | regular user with write access | Create works; Grafana scope creation refused | regular |
| SO-21 | Permissions and Safety | Stack page | admin | Create Grafana scope available; Favourites panel | admin |
| SO-22 | Use | Stack page, Favourites panel | complete stack | Starred default, drag handles, add and edit form | admin |
| SO-23 | Permissions and Safety | Stack page, Grafana panel | complete stack | Local admin password masked with Reveal and Copy links (password blurred) | admin |
