# Screenshots needed: Kubernetes Upgrader

Draft by Raman and Claude from the extension repo (UI component names and README). Bhushan: please correct and complete this list on your branch, and verify each step in QA (https://ai-helpdeskv2-qa01.ai-qa-automation-apps.duplocloud.net/, workspace `agents-qa`). Use test data only: no real account IDs, tokens or customer data.

| ID | Doc page | Menu path or URL | Setup steps and test data | What to show or highlight | Role |
| --- | --- | --- | --- | --- | --- |
| KU-01 | Set Up | Agent Marketplace > Kubernetes Upgrader | none | Agent card and the Activate button | admin |
| KU-02 | Set Up | Admin menu (currently DevOps menu, DUPLOAI-5602) | agent activated | Kubernetes Upgrader entry in the menu | admin |
| KU-03 | Set Up | Kubernetes Upgrader > Kubernetes Clusters > Add Kubernetes Cluster | QA AWS scope with a test EKS cluster | Scope and region pickers | admin |
| KU-04 | Set Up | same form | pick scope, region | Cluster list loaded and the label field | admin |
| KU-05 | Use | Cluster > Add Job | registered test cluster | The three upgrade choices (Control Plane, Add-on, Worker Node Swap) | admin |
| KU-06 | Use | Add Job form | choose a target version | Upgrade Path preview with steps | admin |
| KU-07 | Use | Add Job form | choose Worker Node Swap | Run pre-flight checks results and the risk checkbox | admin |
| KU-08 | Use | Job page, status WaitingForApproval | create a plan | Plan review: path, add-ons, worker groups, pre-flight | admin |
| KU-09 | Use | Approve dialog | click Approve | Type-the-cluster-name confirmation and countdown | admin |
| KU-10 | Use | Job page, status running | approve a small test job | Banner, Upgrade Path stepper, phase cards, node table | admin |
| KU-11 | Use / Troubleshooting | Job page paused | optional: test credential expiry | Paused banner naming the scope | admin |
| KU-12 | Permissions and Safety | Clusters list | read-only test user | Add Kubernetes Cluster disabled with the message | read-only |
| KU-13 | Permissions and Safety | Job page | read-only test user | Approve, Reject, Cancel disabled; kubectl console replaced by a message | read-only |
| KU-14 | Permissions and Safety | Job page | regular user with create but not approve | Create job works, Approve disabled | regular |
| KU-15 | Use | Job page, Ask AI panel | open the panel | Panel with a sample question | admin |
| KU-16 | Use | Job page, kubectl console | run `get nodes` | Console output | admin |
