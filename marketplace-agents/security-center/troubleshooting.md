---
description: Common problems with Security Center and how to fix them.
---

# Troubleshooting and FAQ

## Common problems

| What you see | What it means | What to do |
| --- | --- | --- |
| **"Security Center isn't set up yet"** banner | No AWS account is connected to the workspace. | Ask your administrator to connect a cloud account in **Settings > Cloud accounts**. |
| **A button is disabled, with a message about permission** | Your permission sets do not include the action. | Ask an administrator for the permission (see [Permissions and Safety](permissions-and-safety.md)). |
| **403 or 404 when you open or change something** | You do not have the permission, or cannot see the resource. | Ask an administrator. |
| **Many compliance checks show Error** and the score is low | The AWS connection lacks read permissions, a service is unavailable, or a region is opted out. The Coverage tab lists each failed read and its AWS error code. | Add the missing read permissions (see [Set Up](set-up.md)) and re-assess. |
| **Cannot change accounts, regions, criteria or tag filter** | They are frozen after create so the history stays comparable. | Create a new scan. |
| **Re-assess says a run is in progress** | A run is queued, running or waiting. | Wait for it to finish. |
| **No CVEs appear** | CVEs need continuous monitoring on for the account, with Inspector selected, in the regions where the event rule and queue are in place. A region's first sweep can take a few minutes. | Check the account page in **Settings > Cloud accounts**. Inspector also needs `inspector2:ListFindings`. |
| **Data flow shows CVEs as waiting** | The region's event rule predates CVE support. | It is upgraded automatically within about 5 minutes, or select **Re-apply now** on the account. |
| **Get a fix is blocked** | The account has a write connection but no read-only connection. | Set a read-only connection in the account's **Fix access** card. |
| **Approve and run is disabled** | Write access is not attached, the fix has already run, or you lack the permission. | Select **Attach write access** first. A CLI fix that can never be approved (no write connection, or one that was renamed or deleted) can be replaced with **Try a new fix** on the gap. |
| **"The proposed command changed since you reviewed it"** | The stored command is not the one on your screen. | Reload the fix, read the command, and approve it again. |
| **A fix falls back to an AWS CLI command** | The resource was not found in your Terraform or CloudFormation. Terraform needs state in a plain S3 backend with a fixed bucket and key, readable by the account's connection. | Fix the repository settings, or accept the command. The fix page shows how the agent chose, and lookups that failed show as "couldn't check". |
| **CloudFormation fix "could not patch automatically"** | The template uses a macro or transform, JSON or CDK, flow-style properties, or the rule is a separate resource. | Apply the change yourself, using the proposed section as a guide. |
| **Repositories show "couldn't check"** | They are not reachable with the GitHub connection. All repositories must use the same connection. | Fix access or the connection in **Settings > General > Code repositories**. |
| **Impact analysis cannot start: no usable trail** | The account has no logging trail with a readable S3 bucket that records management events. | Pick another trail, or a log archive connection for a bucket in another account. There is no event-history fallback. |
| **"Can't read bucket: AccessDenied"** in coverage | The connection cannot read the trail bucket. | Grant `s3:ListBucket`, `s3:GetObject` and, for an encrypted bucket, `kms:Decrypt`. |
| **Analysis ends Inconclusive with "region-days unread"** | The window was too large to finish reading, or the trail has gaps. | Narrow the window, or use **Edit window** to read the missing days. |
| **Containment controls are disabled: "Set up a write connection"** | The account has no write connection. | Set one in **Fix access**. |
| **Cannot delete an analysis** | A containment from it is still in effect. | Undo the containment first. |

<!-- VERIFY: messages above come from code and README text, not a live run. Confirm in QA (screenshots SC-29 to SC-31). -->

## FAQ

**Does it change my AWS account?** Compliance scans and impact analyses do not. Applying an account profile, approving a CLI fix and applying a containment action do, and each is a separate permission. See [Permissions and Safety](permissions-and-safety.md).

**Does a good score mean I am SOC 2 compliant?** No. It means clean against these checks. SOC 2 also covers people, process and systems outside AWS.

**What does "Not detected in AWS" mean?** An AWS-native capability was not found. Another tool may cover the objective, so it is not shown as a failure.

**Can I assess the other criteria?** Not yet. Availability, Confidentiality, Processing Integrity and Privacy are shown disabled.

**Can a pull request be merged for me?** No. Security Center never merges.

**Does turning a service off in Security Center turn it off in AWS?** No, with one exception. An administrator can confirm turning off AWS Config, GuardDuty or Inspector, and only where Security Center turned them on.

**Is the Slack alert per CVE?** No. CVEs only post in a daily digest.

<!-- VERIFY: FAQ is a first guess. Darren to add the questions customers actually ask. -->
