---
description: Common problems with Security Center, the messages you see, and how to fix them.
---

# Troubleshooting and FAQ

## Setup and access

| Problem or message | Cause | Fix |
| --- | --- | --- |
| **Security Center isn't set up yet.** Ask your administrator to connect a cloud account and assign it to this workspace. | No AWS account is assigned to this workspace, or the workspace has no connection to it. | An administrator assigns the account in **AI Admin > Security Center > Cloud accounts**, and attaches a connection to the account to this workspace. See [Set Up](set-up.md#assign-each-aws-account-to-a-workspace). |
| **AWS account … isn't assigned to a workspace yet** or **… is managed in another workspace** | Each account belongs to one workspace. Only that workspace can use it. | Ask an administrator to assign the account to your workspace, or work from the workspace that owns it. |
| **No AWS connections on the Admin Workspace** (on Cloud accounts) | The AWS connections aren't attached to the Admin Workspace, so AI Admin can't see the accounts. | Attach each AWS connection's scope to the Admin Workspace. |
| **Cloud account settings are managed by administrators in AI Admin → Security Center → Cloud accounts.** | Account settings and fix access are administrator-only. | Ask an administrator to make the change. |
| **You don't have access to …** or **You don't have permission to do this.** | Your permission sets don't include what you tried. | Ask a workspace admin to grant it. See [Permissions and Safety](permissions-and-safety.md#who-can-do-what). |
| **Connection '…' is not attached to this workspace.** | A connection chosen in Settings isn't attached to the right workspace. Slack, Jira and GitHub in AI Admin must be attached to the Admin Workspace. | Attach the connection's scope, then save again. |
| **The platform's GitHub connection is not attached to this workspace, and repositories use it.** | The workspace uses the platform's repositories but doesn't have the GitHub connection. | Ask an administrator to attach the GitHub connection to the workspace. |

## Scans

| Problem or message | Cause | Fix |
| --- | --- | --- |
| A check shows **Error** and the score is lower than expected | The connection couldn't read what the check needs. A failed read counts against the score. | Open the **Coverage** tab to see which reads failed and why. Add the missing read permission to the connection. The AWS managed policies `ReadOnlyAccess` and `SecurityAudit` together cover them. |
| **An assessment run is already in progress … Wait for it to finish, then re-assess.** | A run is still going. | Wait for it to finish, then select **Run again**. |
| Resources in a region aren't in the results | The scan reads only the regions you chose. | Create a new assessment that includes the region. The regions of an existing one can't change. |

## Fixes

| Problem or message | Cause | Fix |
| --- | --- | --- |
| **No write connection is set for account …, so this command can't run.** | The account has no write connection in Fix access. | An administrator sets one in the account's **Fix access** card in AI Admin. Then go back to the gap and select **Plan a new fix**. |
| **This account has a write connection but no read-only connection.** | Every fix starts with the read-only connection, and the account has none. | An administrator sets the read-only connection in the account's **Fix access** card. |
| **The proposed command changed since you reviewed it. Reload the fix, read the command and approve it again.** | The stored command changed after you loaded the page. | Reload the page, read the command again, and approve it. |
| **This browser cannot check the command before it runs (it needs a secure connection), so it was not run.** | The page must check the command before running it, which needs HTTPS. | Open DuploCloud over `https://`. |
| **This fix failed and can't be retried — start a new fix from the gap.** | A fix runs once. | On the gap, select **Plan a new fix**. |
| **The drafted command was not run** | The command the agent drafted didn't pass the safety check before running. | On the gap, select **Plan a new fix**. |
| **The template could not be patched automatically — see the warnings above.** | Security Center couldn't edit the CloudFormation template safely. | Read the warnings, and make the change in the template yourself. |
| A fix comes back as an AWS CLI command although you use Terraform | Security Center couldn't match the resource to your Terraform state. The state must be in an S3 backend that the account's read-only connection can read, in a repository listed in Settings. | Check that the repository is listed under **Code repositories** and that its state is readable, then plan the fix again. |

## Impact analysis

| Problem or message | Cause | Fix |
| --- | --- | --- |
| **This account has no CloudTrail trail.** | An impact analysis needs a trail whose logs it can read. | Create a CloudTrail trail that records management events and delivers to an S3 bucket, or ask an administrator to turn on CloudTrail for the account. |
| **No trail logs management events** or **No logging trail delivers to an S3 bucket.** | The trails the account has can't be used. | Change a trail so it records management events and delivers to S3. |
| **That connection can't read bucket …** | The connection can't read the trail's bucket, often because the bucket is in another AWS account, such as an organization's log archive. | Under **Read it with**, choose a connection that can read the bucket. |
| **Couldn't find this account's folder in bucket … — the log archive connection needs s3:ListBucket on AWSLogs/.** | The trail is an organization trail whose bucket is in another AWS account. | Under **Read it with**, choose a connection to the log archive account that can list and read `AWSLogs/` in that bucket. |
| **Containment needs a write connection for this account** | Containment uses the account's write connection. | An administrator sets one in the account's **Fix access** card. |
| **This action can't be undone.** | Delete and terminate actions are permanent. | Nothing to fix. Check the target before you confirm. |
| **Could not finish reading; … region-days unread** | Some CloudTrail logs couldn't be read in time. | Look at the **Coverage** tab, then run the analysis again or narrow the window. |
| **Re-run this analysis — it was created before trail-bucket support.** | The analysis is from an older version. | Start a new impact analysis. |

## Notifications

| Problem or message | Cause | Fix |
| --- | --- | --- |
| **Slack did not accept the message.** (on the test send) | The bot token is wrong, lacks the `chat:write` scope, or the app isn't in the channel. | Check the Slack connection and invite the app to the channel. |
| No Jira tickets are created | Jira tickets are off, or the workspace has no Jira project key. | An administrator turns on **Create a Jira ticket for each new gap** in AI Admin. Set the workspace's project key in **Security Center > Settings > Jira tickets**. |
| The daily CVE digest switch is disabled | No Slack connection is chosen. | An administrator chooses a Slack connection in **AI Admin > Security Center > Settings** first. |

## FAQ

**Does Security Center change my AWS account?** Compliance scans and impact analyses don't. Applying a security profile (administrators only), running an approved AWS CLI fix, and containment do. See [Permissions and Safety](permissions-and-safety.md).

**Does a good score mean we are SOC 2 compliant?** No. It means clean against Security Center's checks. SOC 2 also covers people, processes and systems outside AWS.

**What does "Not detected in AWS" mean?** An AWS-native capability wasn't found. Another tool may cover the same objective, so it isn't counted as a problem.

**Can I check the other SOC 2 criteria?** Not yet. Availability, Confidentiality, Processing Integrity and Privacy are marked **Coming soon**.

**Why can't another workspace scan our account?** Each AWS account belongs to one workspace, so two workspaces never scan and fix the same account. An administrator can move it.

**Does Security Center merge pull requests?** No. You review and merge them yourself.

**Does turning a service off in Security Center turn it off in AWS?** Only what Security Center turned on itself, and only when an administrator does it. Anything that was already on stays on.

**Can I connect Jira?** Yes. An administrator connects Jira once for the platform, and each workspace sets its own project key. Security Center can then open a ticket for each new gap, or for gaps you select, and keeps it updated as the gap is fixed. See [Set Up](set-up.md#connect-github-slack-and-jira-optional).

**Is there a Slack alert for each CVE?** No. CVEs are posted only in the daily digest.
