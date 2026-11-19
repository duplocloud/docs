---
description: What you need before you start, how to activate Security Center, connect an AWS account, and the AWS permissions it needs.
---

# Set Up

## Before you start

- An **AWS connection (scope)** in your workspace for each AWS account you want to cover. Until one is connected, every Security Center page except Settings shows "Security Center isn't set up yet. Ask your administrator to connect a cloud account".
- **Read permissions** on that connection (see below). A missing read permission does not fail a scan. The check that needs it shows as **Error** and lowers the score.
- Optional, to turn on continuous monitoring: permission to change account-level security settings in AWS (see "Permissions to turn on continuous monitoring").
- Optional, for fixes as pull requests: a **GitHub connection** and the repositories that hold your Terraform or CloudFormation. Repositories are listed in Settings, in order, and must all be reachable with the same GitHub connection.
- Optional, for fixes as AWS CLI commands: a separate **write connection** for the account (see "Fix access").
- Optional: a Slack connection, and a Jira connection.
- **Permissions** for the people who will use it. Security Center uses the platform's permission sets, and ships none of its own. See [Permissions and Safety](permissions-and-safety.md).

<!-- VERIFY: exact prerequisites for the Slack connection (the settings page shows numbered setup steps) and GitHub connection rights. Darren to add the customer-facing steps. -->

## Activate Security Center

1. Open the **Agent Marketplace** and find **Security Center**.
2. Select **Activate** and confirm.
3. When it finishes, a **Security Center** section appears in the left navigation with Overview, Impact analyses, Data flow, Gaps & Remediation, CVEs, Plans and fixes, Compliance and Settings.

<!-- VERIFY: exact marketplace steps and button names (screenshots SC-01 and SC-02). The manifest also adds a "Security Center > Settings" entry under the Admin menu for the platform policy (admin only). -->

## Connect an AWS account

1. Open **Security Center > Settings > Cloud accounts**. It lists every AWS account connected to the workspace with a status (Protected, Not set up, Problem, Applying).
2. Open an account to see its regions, one card per service (Security Hub, AWS Config, CloudTrail, GuardDuty, Inspector, IAM password policy, continuous monitoring), and its **Fix access** card.
3. Turn on the services you want and save. Saving applies the profile to the AWS account.

{% hint style="warning" %}
Applying a profile changes the AWS account: it turns services on and creates resources there. It needs the separate **Apply an account security profile** permission. Turning a service off in Security Center does not turn it off in AWS, with one exception for administrators described in [Permissions and Safety](permissions-and-safety.md).
{% endhint %}

<!-- VERIFY: the Cloud accounts page labels and statuses (screenshots SC-03 and SC-04). -->

### Permissions to turn on continuous monitoring

Applying a profile uses these AWS actions, from the code that does the work. Grant only what you need for the services you turn on.

| Service | AWS actions |
| --- | --- |
| Security Hub | `securityhub:EnableSecurityHub`, `securityhub:DescribeHub`, `securityhub:BatchEnableStandards`, `securityhub:GetEnabledStandards`, `securityhub:CreateMembers`, `securityhub:InviteMembers`, `securityhub:ListMembers`, `securityhub:ListInvitations`, `securityhub:AcceptAdministratorInvitation`, `securityhub:GetAdministratorAccount` |
| AWS Config | `config:PutConfigurationRecorder`, `config:StartConfigurationRecorder`, `config:StopConfigurationRecorder`, `config:PutDeliveryChannel`, `config:PutConformancePack`, `config:DescribeConfigurationRecorders`, `config:DescribeConfigurationRecorderStatus`, `config:DescribeDeliveryChannels` |
| CloudTrail | `cloudtrail:CreateTrail`, `cloudtrail:StartLogging`, `cloudtrail:DescribeTrails`, `cloudtrail:GetTrailStatus` |
| GuardDuty | `guardduty:CreateDetector`, `guardduty:UpdateDetector`, `guardduty:GetDetector`, `guardduty:ListDetectors` |
| Inspector | `inspector2:Enable`, `inspector2:Disable`, `inspector2:BatchGetAccountStatus`, `inspector2:ListFindings` |
| IAM password policy | `iam:GetAccountPasswordPolicy`, `iam:UpdateAccountPasswordPolicy`, `iam:CreateServiceLinkedRole` |
| Log storage | `s3:CreateBucket`, `s3:PutBucketPolicy`, `s3:PutEncryptionConfiguration`, `s3:PutBucketPublicAccessBlock`, `kms:CreateKey`, `kms:CreateAlias`, `kms:DescribeKey`, `kms:EnableKeyRotation`, `kms:PutKeyPolicy`, `kms:ListAliases` |
| Event stream | `events:PutRule`, `events:PutTargets`, `events:RemoveTargets`, `events:DeleteRule`, `sqs:CreateQueue`, `sqs:GetQueueUrl`, `sqs:SetQueueAttributes`, `sqs:DeleteQueue`, `ec2:DescribeRegions` |

<!-- VERIFY: this list is the AWS SDK calls found in the account setup code (AwsSdkSecurityApi.cs), converted to IAM action names by hand. The extension has no ready-made IAM policy. Darren to confirm the exact action names and whether a policy or CloudFormation template is published for customers. -->
<!-- VERIFY: which of these resources the extension creates in the customer account and what they are called (a trail, a log bucket, a KMS key, an EventBridge rule and an SQS queue per region). Not described by name in the code read. -->

## Permissions for compliance scans (read-only)

A scan makes `describe`, `list` and `get` calls and generates the IAM credential report. It needs read access to the services in the table.

| Area | AWS actions |
| --- | --- |
| Identity | `iam:GetAccountSummary`, `iam:GetAccountPasswordPolicy`, `iam:GenerateCredentialReport`, `iam:GetCredentialReport`, `iam:ListUsers`, `iam:ListMFADevices`, `iam:ListAccessKeys`, `iam:GetAccessKeyLastUsed`, `iam:ListAttachedUserPolicies`, `iam:ListRoles`, `iam:ListEntitiesForPolicy`, `iam:ListPolicies`, `iam:GetPolicyVersion`, `iam:ListGroups`, `iam:ListUserPolicies`, `iam:GetUserPolicy`, `iam:ListRolePolicies`, `iam:GetRolePolicy`, `iam:ListGroupPolicies`, `iam:GetGroupPolicy`, `access-analyzer:ListAnalyzers`, `access-analyzer:ListFindings` |
| Logging and monitoring | `cloudtrail:DescribeTrails`, `cloudtrail:GetTrailStatus`, `cloudtrail:GetEventSelectors`, `config:DescribeConfigurationRecorders`, `config:DescribeConfigurationRecorderStatus`, `config:DescribeDeliveryChannels`, `config:DescribeConfigRules`, `config:DescribeComplianceByConfigRule`, `ec2:DescribeFlowLogs`, `logs:DescribeLogGroups`, `cloudwatch:DescribeAlarms`, `guardduty:ListDetectors`, `guardduty:GetDetector`, `guardduty:ListFindings`, `securityhub:GetEnabledStandards`, `securityhub:GetFindings` |
| Data protection | `s3:GetAccountPublicAccessBlock`, `s3:ListAllMyBuckets`, `s3:GetBucketPublicAccessBlock`, `s3:GetBucketPolicyStatus`, `s3:GetEncryptionConfiguration`, `s3:GetBucketVersioning`, `s3:GetBucketLogging`, `s3:GetLifecycleConfiguration`, `s3:GetBucketPolicy`, `ec2:GetEbsEncryptionByDefault`, `rds:DescribeDBInstances`, `rds:DescribeDBSnapshots`, `rds:DescribeDBSnapshotAttributes`, `kms:ListKeys`, `kms:DescribeKey`, `kms:GetKeyRotationStatus`, `kms:GetKeyPolicy`, `secretsmanager:ListSecrets`, `secretsmanager:DescribeSecret` |
| Network and compute | `ec2:DescribeVpcs`, `ec2:DescribeSecurityGroups`, `ec2:DescribeSecurityGroupRules`, `ec2:DescribeInstances`, `ec2:DescribeVolumes`, `ec2:DescribeSnapshots`, `ec2:DescribeImages`, `elasticloadbalancing:DescribeLoadBalancers`, `elasticloadbalancing:DescribeListeners`, `elasticloadbalancing:DescribeTags`, `eks:ListClusters`, `eks:DescribeCluster`, `lambda:ListFunctions`, `lambda:GetFunctionUrlConfig`, `lambda:GetPolicy`, `ecr:DescribeRepositories`, `ecr:GetRegistryScanningConfiguration`, `ecr:GetRepositoryPolicy` |
| Patching and other | `ssm:DescribeInstanceInformation`, `ssm:DescribeInstancePatchStates`, `inspector2:BatchGetAccountStatus`, `sns:ListTopics`, `sns:GetTopicAttributes`, `sqs:ListQueues`, `sqs:GetQueueAttributes`, `elasticfilesystem:DescribeFileSystems`, `redshift:DescribeClusters`, `acm:ListCertificates`, `account:GetAlternateContact` |
| Which stack created a resource | `cloudformation:DescribeStacks`, `cloudformation:ListStackResources`, `cloudformation:GetTemplate` |
| Only with the tag filter | `s3:GetBucketTagging`, `rds:ListTagsForResource`, `iam:ListUserTags` |

<!-- VERIFY: rebuilt by hand from the scan skill documentation (check library 2026.10.6). The polled-calls table in the skill is cut off in places, so the list may be incomplete. Darren to confirm against collect.sh. -->

## Fix access

Each account page has a **Fix access** card with two connections that must be different:

- A **read-only connection**: used to investigate. Every fix opens with it, and impact analyses read with it.
- A **write connection**: used only to run approved AWS CLI commands and containment actions. It is never offered on the **Get a fix** form.

Both must be AWS connections that belong to that account. Pull-request fixes (Terraform and CloudFormation) need no write access.

<!-- VERIFY: the platform permissions needed to read or change Fix access (it is its own access node; only admins or a set that names it can change it). Confirm in QA (screenshot SC-05). -->

## Connect GitHub, Slack and Jira (optional)

In **Settings > General**:

- **Code repositories**: add the Terraform or CloudFormation repositories in the order they should be checked, each with its GitHub connection.
- **Notifications**: connect Slack and send a test message. Turn on the daily CVE digest if you want it.
- **Jira tickets**: pick the Jira connection and a project key, then **Test connection**. The Jira connection is a provider connection with a service-account API token that can read the project and create, comment on and transition issues.

<!-- VERIFY: step names, and exactly how a customer registers the Jira provider connection (provider type "Other", metadata ticketing=true, account id = site URL, credential api_token, according to the README). Darren to give customer wording. -->

## Grant access

Give the people who will use it permission sets that cover Security Center. The extension ships no permission sets. See [Permissions and Safety](permissions-and-safety.md) for what to grant and the pitfall with the action wildcard.

Next: [Use](use.md).
