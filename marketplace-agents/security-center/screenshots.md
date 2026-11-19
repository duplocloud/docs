# Screenshots needed: Security Center

Draft by Raman and Claude from the extension repo, branch `dev`, commit ce185ae8911343cd309571828fe57240b59d8f50 (version 0.15.30): UI component names, README and skill docs. Darren: please correct and complete this list on your branch, and verify each step in QA (https://ai-helpdeskv2-qa01.ai-qa-automation-apps.duplocloud.net/, workspace `agents-qa`). Use test data only: no real account IDs, tokens or customer data. Use a sandbox AWS account and a test GitHub repository.

| ID | Doc page | Menu path or URL | Setup steps and test data | What to show or highlight | Role |
| --- | --- | --- | --- | --- | --- |
| SC-01 | Set Up | Agent Marketplace > Security Center | none | Agent card and the Activate button | admin |
| SC-02 | Set Up | Left navigation | agent activated | The Security Center section with its eight items | admin |
| SC-03 | Set Up | Security Center > Settings > Cloud accounts | one sandbox AWS connection | List of accounts with status | admin |
| SC-04 | Set Up | Account page | open one account | Region list, one card per service, switches, Changes your AWS accounts tag, Re-apply now | admin |
| SC-05 | Set Up | Account page > Fix access card | two different AWS connections | Read-only and write connection pickers | admin |
| SC-06 | Use | Security Center > Overview | some gaps and one scan | Stat tiles, Patch deadlines card | admin |
| SC-07 | Use | Compliance > Add | open the form | Name, accounts with "n of 5", regions with "n of 6", criteria with four disabled | admin |
| SC-08 | Use | Compliance > Add (lower part) | scroll | Tag filter, severity floor, notes, the GRC provider picker | admin |
| SC-09 | Use | Compliance > scan > Dashboard | finished scan, sandbox account, 1 region | Score dial, severity tiles, criteria bars, history line | admin |
| SC-10 | Use | Scan > Findings | same | Table with facets, and a Problem found and a Not detected in AWS row | admin |
| SC-11 | Use | Scan > Controls and Coverage | use a connection missing some read permissions | Controls with Not evidenced in AWS; Error rows first in Coverage | admin |
| SC-12 | Use | Scan > History | re-assess at least twice | Score line and new and resolved checks | admin |
| SC-13 | Use | Gaps & Remediation | several gaps | Table with status and severity chips | admin |
| SC-14 | Use | A gap page | open one | Facts, controls, Get a fix button | admin |
| SC-15 | Use | Gap > Get a fix | open the form | Approach picker with Let the agent find it as default | admin |
| SC-16 | Use | Fix with a pull request | test repo with Terraform and S3 state | Pull request link, diff, how the agent chose | admin |
| SC-17 | Use | Fix with an AWS CLI command | a check with a curated command | Command, explanation, warnings, Attach write access, Approve and run | admin |
| SC-18 | Use | Plans and fixes | one grouped plan | Plan list with Needs more planning and Analyze scope | admin |
| SC-19 | Use | CVEs | Inspector on a test instance | Table with due dates and severity chips | admin |
| SC-20 | Use | Impact analyses > New analysis | sandbox account with a logging trail | Wizard: account, window, seeds, trail choice with "Can read a log file from this bucket" | admin |
| SC-21 | Use | Analysis result | finished analysis | Verdict, attack status banner, coverage strip, graph and timeline | admin |
| SC-22 | Use | Analysis > node > containment | test IAM user as a seed | Quarantine as the default action, and the confirmation dialog | admin |
| SC-23 | Use | Analysis > Edit window | finished analysis | Narrow and widen options | admin |
| SC-24 | Use | Settings > General | open the page | Sections: Frameworks, Automation, Notifications, Scanning, SLAs, Repositories, Always-attached | admin |
| SC-25 | Permissions and Safety | Gaps, a gap, and a fix page | read-only test user (a set with GET and an empty Actions field) | Disabled Get a fix, Approve and run and Attach write access with the permission message | read-only |
| SC-26 | Permissions and Safety | Same screens | regular user with Triage rights | Ignore and close available, Get a fix disabled | regular |
| SC-27 | Permissions and Safety | Same screens | user with propose-fix but not execute-fix | Get a fix works, Approve and run disabled | regular |
| SC-28 | Permissions and Safety | Platform permission set editor | admin | The Security Center branch, rules, verbs and the Actions field | admin |
| SC-29 | Troubleshooting | Any page | workspace with no AWS account | The "isn't set up yet" banner | admin |
| SC-30 | Troubleshooting | Fix page after the command changed | edit the stored command (test only) | The "changed since you reviewed it" message | admin |
| SC-31 | Troubleshooting | Impact analysis wizard | account with no usable trail | Start disabled with the reason | admin |
