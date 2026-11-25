---
description: What you need before you start, how to activate AWS Cost Intelligence from the Agent Marketplace, and how to connect it to your accounts.
---

# Set Up

## Before you start

- **Cost Explorer** turned on in your AWS payer (management) account, or in the single account you want to cover. It can take up to 24 hours to fill the first time.
- **Resource-level data at daily granularity** turned on in the Cost Management preferences. Without it, Resource Explorer is empty and the Action Center cannot confirm savings.
- **Cost Optimization Hub** enabled (include member accounts). Without it, the Optimisation tab and most Action Center items are empty.
- **Cost allocation tags** activated in Billing for the tags you report on (for example `Team`, `Owner`).
- An **AWS read-only role or user** for billing (see below), registered in DuploCloud as an AWS provider with a scope attached to your workspace.
- A DuploCloud **platform administrator** to add the cost data source. See [Permissions and Safety](permissions-and-safety.md).
- An **AI model** available in your workspace, only if you want Ask AI, custom dashboards, adding a policy or Helpdesk analysis.

{% hint style="info" %}
Missing AWS permissions do not fail the sync. The tab that needs the missing action shows a notice naming it, and the source page lists the warnings.
{% endhint %}

<!-- VERIFY: Setup takes about an hour plus up to 24 hours for Cost Explorer (docs/SETUP.md). Confirm this estimate is still right before publishing. -->

### Running cost in AWS

AWS Cost Intelligence only calls AWS from a background sync, never when someone views a page. Almost all of the cost is Cost Explorer API requests, which AWS bills at about US$0.01 per request. The extension's own estimate is about US$70 a month for a 45-account organisation with every dashboard on the default 6-hour refresh, about US$37 for a single account, plus a one-time US$1 to US$10 while history fills in. Refreshing once a day roughly halves it. Each source page shows the Cost Explorer requests and estimated spend so far.

<!-- VERIFY: figures are from docs/RUNNING-COST.md, which cites sync code 0.56.64 and prices as of November 2026; the manifest is 0.58.7. Confirm they still hold for the release. The repo does not say whether the agent itself is free or paid. -->

### AWS permissions by feature

All of these are read actions.

| Feature | AWS actions |
| --- | --- |
| Billing source role (required) | `sts:GetCallerIdentity`, `ce:GetCostAndUsage`, `ce:GetCostForecast`, `ce:GetTags`, `ce:ListCostAllocationTags`, `ce:ListCostAllocationTagBackfillHistory` |
| Resource costs and Action Center confirmation | `ce:GetCostAndUsageWithResources` |
| Commitments | `ce:GetSavingsPlansUtilization`, `ce:GetSavingsPlansUtilizationDetails`, `ce:GetSavingsPlansCoverage`, `ce:GetSavingsPlansPurchaseRecommendation`, `ce:GetReservationUtilization`, `ce:GetReservationCoverage`, `ce:GetReservationPurchaseRecommendation` |
| Anomalies and recommendations | `ce:GetAnomalies`, `cost-optimization-hub:ListRecommendations`, `cost-optimization-hub:GetPreferences`, `cost-optimization-hub:ListRecommendationSummaries`, `cost-optimization-hub:GetRecommendation` |
| Budgets and invoices | `budgets:ViewBudget`, `invoicing:ListInvoiceSummaries` |
| Accounts and names | `organizations:DescribeOrganization`, `organizations:ListAccounts`, `organizations:ListTagsForResource`, `ec2:DescribeTags` |
| Resource Ownership (optional) | `cloudtrail:LookupEvents`, `cloudtrail:DescribeTrails`, `cloudtrail:GetEventSelectors`, `cloudtrail:GetTrailStatus`, `cloudtrail:ListTags`, `ec2:Describe*` for instances, volumes, snapshots, images, addresses, NAT gateways, VPCs, endpoints and network interfaces, `eks:ListClusters`, `eks:DescribeCluster`, `eks:ListNodegroups`, `eks:DescribeNodegroup`, `autoscaling:DescribeAutoScalingGroups`, `rds:DescribeDBInstances`, `rds:DescribeDBClusters`, `rds:DescribeDBSnapshots`, `rds:DescribeDBClusterSnapshots`, `cloudwatch:GetMetricData`, and read-only calls to CloudWatch Logs, Elastic Load Balancing, ECR, KMS, Route 53 and S3 for the account scan |
| Helpdesk analysis (optional) | A separate analysis role per account with `Describe*` and `List*` on the services Action Center items are about, CloudWatch metrics, and cost and recommendation reads. It explicitly denies reading data and secrets |

<!-- VERIFY: source is docs/ROLES.md (complete JSON policies). Confirm with the owner that the list is current, and whether the CloudFormation templates are published to customers. The Resource Ownership row is abbreviated; the full policy has more S3, KMS, ECR and ELB read actions. -->

AWS's managed `AWSBillingReadOnlyAccess` policy covers most of the billing role but not Budgets, Organizations or `ec2:DescribeTags`. For the analysis role, do not use AWS's managed `ReadOnlyAccess`: it also reads data such as S3 objects and Lambda environment variables.

### Create the roles

The extension ships two CloudFormation templates that create only IAM roles with read-only policies.

1. In the payer account (or the single account), deploy the **billing** template. Choose `IamRole` as the credential type and give it the ARN of the identity your DuploCloud platform runs as. Note the **RoleArn** and **AccountId** outputs.
2. In an organisation that uses Resource Ownership or Helpdesk analysis, deploy the **member** template as a StackSet from the management account to the organisational units you want. It creates a member read role (trusted only by the billing role) and, if chosen, an analysis role in every member account.

A single account needs only step 1. You can also create the same roles by hand.

<!-- VERIFY: template file names (cost-intelligence-billing.yaml, cost-intelligence-member.yaml) and where customers get them. Ask the owner how customers receive them after activation. -->

## Activate AWS Cost Intelligence

1. Open the **Agent Marketplace** and find **AWS Cost Intelligence**.
2. Select **Activate** and confirm.
3. When it finishes, it appears in the menu under **FinOps** as **Cost Intelligence**.

<!-- VERIFY: marketplace steps and button names are copied from the pilot and are not in this repo. The menu path FinOps > Cost Intelligence comes from the manifest. Screenshots CI-01 and CI-02. -->

## Register the AWS credential

1. Open the app switcher, then **AI Admin > Providers > IT > Cloud** and select **Add**.
2. **Provider Details**: a name, type **AWS**, and the account ID of the payer (or single) account. Select **Next**.
3. **Credentials**: for an IAM role, enter the role ARN. Select **Next**.
4. **Scope**: a name and a region (`us-east-1` is fine). Select **Create**.
5. When **Attach Scope to Workspaces** opens, pick the workspace that will hold the cost data and select **Attach**. Do not skip this step. The extension only lists scopes attached to the workspace you are in.

<!-- VERIFY: wizard labels from docs/SETUP.md B1, not checked against the live UI (screenshots CI-03, CI-04). -->

## Grant access

Give people the permissions in [Permissions and Safety](permissions-and-safety.md). Refreshing cost data and exporting cost rows are separate named actions (`finops.sync`, `finops.export`) and are not part of ordinary read or edit access.

## Add your first cost data source

1. A platform administrator opens **FinOps > Cost Intelligence** and selects **Add Cost Data Source**.
2. Fill in the form:

| Field | What to enter |
| --- | --- |
| Name | Anything, 2 to 60 letters, numbers and hyphens |
| AWS Scope | The scope you attached. If it is missing, it is not attached to this workspace |
| Home Region | `us-east-1` unless you have a reason not to. Commercial regions only |
| Cost Metric | Amortized (default) or Unblended |
| Accounts covered | Auto (default), Organization or Single account |
| Lookback Months | 13 by default, up to 38 |
| Cost Allocation Tag Keys | Tags you activated, up to 20 |

3. Under **Advanced** (closed by default) you can set the **Refresh Schedule** (a five-field cron in UTC, at most hourly, default every 6 hours), the **Member Account Role** and **Member Role External ID** (only for Resource Ownership), whether to **connect member accounts for Helpdesk analysis automatically**, and an **Assume Role ARN** if the scope's credential is in another account.
4. Select **Create**. The first sync starts straight away. The current and previous month are ready after it; older months fill in over the next few syncs.

<!-- VERIFY: field names and defaults come from docs/USER-GUIDE.md and the form code; confirm the live form (screenshots CI-05, CI-06). -->

## Check it works

- The source page shows status **Complete**, with accounts and billing months listed.
- Warnings on the source page name any action the role could not call.
- Last month's total on **Cost and Usage > Billing Summary** matches Cost Explorer for the same cost metric.

## Optional: Jira or ClickUp tickets

Action Center tickets go to Helpdesk by default. To use Jira or ClickUp, a DuploCloud administrator registers a provider in **AI Admin > Providers** (category **Other**) and attaches its scope to the workspace. Use an Atlassian service account (Jira Cloud) or a dedicated bot member (ClickUp), never a person's own token, with access to the one project or List only. Then choose it in the Action Center **Settings**.

<!-- VERIFY: the exact credential keys and scopes are in the extension README (Integrating ClickUp and Jira). Decide whether to include them here or on a separate reference page. Note that DuploCloud does not use Jira internally; this is for customers. -->

Next: [Use](use.md).
