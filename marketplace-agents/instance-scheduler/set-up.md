---
description: What you need before you start, how to activate Instance Scheduler from the Agent Marketplace, and how to connect it to your accounts.
---

# Set Up

## Before you start

- An **AWS credential scope** in your workspace that points to the AWS account with the instances and databases you want to schedule. Instance Scheduler acts with that scope's credentials.
- **IAM permissions** on that scope's identity for the actions listed below. Instance Scheduler creates IAM roles and EventBridge schedules (and, for RDS, Lambda functions and a Secrets Manager secret) in that account, so the identity needs more than read access.
- An **administrator** in your workspace to approve schedules requested by other users (see [Permissions and Safety](permissions-and-safety.md)).

<!-- VERIFY: the repo README only says the credentials "need permission for EC2/RDS, IAM, EventBridge Scheduler, Lambda and STS (GetCallerIdentity)" and gives no policy. The list below is derived from the aws commands in the two setup scripts. Confirm it is complete, and whether DuploCloud publishes a ready-made policy or CloudFormation template. -->

### AWS permissions for the scope identity

| Feature | AWS actions |
| --- | --- |
| Find targets in the forms | `ec2:DescribeInstances`, `ec2:DescribeRegions`, `autoscaling:DescribeAutoScalingGroups`, `rds:DescribeDBInstances`, `rds:DescribeDBClusters`, `sts:GetCallerIdentity` |
| EC2 and Auto Scaling schedules | `scheduler:CreateSchedule`, `scheduler:DeleteSchedule`, `iam:CreateRole`, `iam:GetRole`, `iam:PutRolePolicy`, `iam:ListRolePolicies`, `iam:DeleteRolePolicy`, `iam:ListAttachedRolePolicies`, `iam:DetachRolePolicy`, `iam:DeleteRole`, `iam:PassRole` |
| Run now (EC2 and Auto Scaling) | `ec2:StopInstances`, `ec2:StartInstances`, `ec2:RebootInstances`, `autoscaling:UpdateAutoScalingGroup` |
| RDS schedules | The schedule and role actions above, plus `lambda:CreateFunction`, `lambda:GetFunction`, `lambda:UpdateFunctionCode`, `lambda:UpdateFunctionConfiguration`, `lambda:AddPermission`, `lambda:RemovePermission`, `lambda:DeleteFunction`, `secretsmanager:CreateSecret`, `secretsmanager:PutSecretValue`, `secretsmanager:DescribeSecret`, `secretsmanager:DeleteSecret` |
| RDS run now, snapshots and clean-up | `rds:StopDBInstance`, `rds:StartDBInstance`, `rds:StopDBCluster`, `rds:StartDBCluster`, `rds:CreateDBSnapshot`, `rds:CreateDBClusterSnapshot`, `rds:DescribeDBSnapshots`, `rds:DescribeDBClusterSnapshots`, `rds:DeleteDBSnapshot`, `rds:DeleteDBClusterSnapshot` |
| Logs in the RDS view | Read access to the `/aws/lambda/rds-` CloudWatch log groups |

<!-- VERIFY: assembled from the setup scripts. iam:PassRole, the Describe actions used by the forms and the log-read action are inferred, not named in the repo. Confirm each with the owner and test with a least-privilege identity. -->

### Roles Instance Scheduler creates in your account

| Role | Trusted by | What it can do |
| --- | --- | --- |
| EC2 scheduler role (one per schedule and region) | EventBridge Scheduler | Run only the chosen action (`ec2:StopInstances`, `ec2:StartInstances` or `ec2:RebootInstances`) on exactly the instances in that schedule. |
| Auto Scaling scheduler role (one per Auto Scaling group) | EventBridge Scheduler | `autoscaling:UpdateAutoScalingGroup` on that one group. |
| RDS Lambda execution role (one per schedule and region) | Lambda | Stop, start and snapshot that schedule's databases, delete the `rds-sched-` snapshots, write CloudWatch Logs, and read one Secrets Manager secret. |
| RDS scheduler roles | EventBridge Scheduler | Invoke that schedule's Lambda functions. Paired schedules can also run RDS start or stop directly. |

Role names start with `duplo-ec2-`, `duplo-asg-` or `rds-` so you can find them. Roles are created if missing and updated in place if you re-provision.

<!-- VERIFY: the repo README lists a Python Lambda named duplo-ec2-{ID} for recurring EC2 schedules. The setup script's AWS scope path creates only an EventBridge Scheduler schedule and a role for EC2 and Auto Scaling (no Lambda). Lambdas are created for RDS (names start rds-snap- and rds-paired-). Confirm which description is current. -->

## Activate Instance Scheduler

1. Open the **Agent Marketplace** and find **Instance Scheduler**.
2. Select **Activate** and confirm.
3. When it finishes, a **Scheduler** section with **EC2** and **RDS** entries appears in the menu.

<!-- VERIFY: exact marketplace steps and button names. The manifest defines a "Scheduler" menu section with EC2 and RDS items (registered as a DevOps resource); confirm the final menu location. Screenshots IS-01 and IS-02. -->

## Grant access

Everyone who can open the workspace can view schedules. Only administrators can create schedules that run directly, run them now, pause or resume them, or delete snapshots. Other users can submit requests that an administrator approves. See [Permissions and Safety](permissions-and-safety.md).

## Choose your credentials

Both create forms ask for an AWS scope. Pick the scope that points to the account you want to schedule. A scope that belongs to another workspace is refused.

<!-- VERIFY: field labels are "AWS Scope" on the EC2 form and "AWS Credential Scope" on the RDS form. Confirm in QA (IS-03, IS-04). -->

Next: [Use](use.md).
