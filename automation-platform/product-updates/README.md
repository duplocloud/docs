---
description: New features and enhancements in DuploCloud
cover: ../../.gitbook/assets/banner dark.png
coverY: 0
---

# Product Updates

_**Last Updated, January 8, 2026**_

* GCP - [GKE Node Pool Scaling](../overview-1/gcp-services/node-pools.md#adding-a-node-pool) — Support scaling node pools down to zero.¹<sup>,</sup>²
* AWS - [Aurora Global Database](../overview/aws-services/database/rds-database/aurora-global-database.md) — Support for globally distributed Aurora clusters.²
* Kubernetes – [Image Update API](../kubernetes-overview/initcontainers-and-sidecar-containers.md) — Support image updates for additional and init containers.¹<sup>,</sup>²
* AWS - [ElastiCache Snapshot Retention](../overview/aws-services/database/elastic-cache.md#updating-snapshot-retention-limit) — Configure snapshot retention limits.¹
* Cost Management - [Custom Resource Tagging](../../overview/use-cases/custom-resource-tags.md) — Apply custom tags to cloud resources.¹<sup>,</sup>²
* Security & Compliance - [Compliance Documents](../security-and-compliance/compliance-reports.md) — Download DuploCloud compliance reports._¹_
* AWS - [ECS Run Task](../../overview/aws-services/containers/ecs-containers-and-task-definitions/#running-a-task-optional) — Allow selecting a capacity provider strategy when running ECS tasks.¹<sup>,</sup>²
* AWS - [S3 Event Notifications](../overview/aws-services/s3-bucket/s3-bucket-notifications.md) — Support for configuring Amazon S3 event notifications.²
* AWS - [Lambda Edit Menu Updates](../../overview/aws-services/lambda/#id-3-toc-title) — Add Maximum Retry Attempts and Maximum Event Age.²
* Kubernetes - [Suspend CronJobs](../../kubernetes/cronjobs.md#suspending-a-cronjob) using a suspend true/false setting.²
* Security - [Attach a default Web Application Firewall (WAF)](../../diagnostics-overview/web-application-firewall-waf.md#setting-a-default-waf-in-a-plan) to all ALBs at the tenant level.²
* General - [Tenant Indicator](../access-control/setting-tenant-topbar-color.md) — Customize the top bar color for individual Tenants.²
* AI - [AI Slack Integration](../../ai-suite/ai-helpdesk/) — Support for integrating DuploCloud AI capabilities with Slack.²
* AWS - [CloudFront Origin Access Control](../overview/aws-services/cloudfront/cloudfront.md) — Use OAC instead of deprecated OAI.¹<sup>,</sup>²
* AWS - [EKS AutoMode](../overview/use-cases/eks-auto-mode.md) — Automatically configure EKS cluster node scaling and management.²
* Identity/Access Management - [Okta Management](../access-control/user-authentication/sso-configuration/okta-management-settings.md) — Manage Okta authentication in DuploCloud.¹
* AWS - [ECS ASG sharing](../overview/aws-services/containers/ecs-containers-and-task-definitions/sharing-ec2-auto-scaling-groups-across-tenants-for-ecs.md) — Sharing EC2 Auto Scaling Groups across Tenants for ECS.¹<sup>,</sup>²
* AWS - [KMS key management](../security-and-compliance/access-control-1/at-rest-encryption/kms-keys.md) — Manage AWS KMS keys at the Tenant level in DuploCloud.¹<sup>,</sup>²
* AWS - [ElastiCache global datastore](../overview/aws-services/database/elastic-cache.md#creating-a-global-datastore) — Support for global ElastiCache clusters.¹<sup>,</sup>²
* AWS - [AMI enhancements](../overview/use-cases/hosts-vms/create-amazon-machine-image-ami.md) — Select, restrict, or share AMIs across Tenants.¹<sup>,</sup>²
* AWS - [Amazon MQ support](../overview/aws-services/amazon-mq.md) — Provision and manage AWS MQ brokers in DuploCloud.¹<sup>,</sup>²
* AWS - [App Runner support](../overview/aws-services/app-runner.md) — Provision and manage AWS App Runner services.¹<sup>,</sup>²
* AWS - [ECS launch and network mode](../../overview/aws-services/containers/ecs-containers-and-task-definitions/#creating-a-task-definition) — Select launch type and network mode for ECS tasks.¹<sup>,</sup>²
* AWS - [OpenSearch upgrade support](../overview/aws-services/elasticsearch.md#managing-an-opensearch-instance) — Upgrade OpenSearch versions within DuploCloud.¹<sup>,</sup>²
* AWS - [EC2 Snapshots](../overview/use-cases/hosts-vms/ec2-snapshots.md) — Support for managing and automating EC2 volume snapshots.¹<sup>,</sup>²
* AWS - [Ingress: Multi-certificate support](../../kubernetes-overview/ingress-loadbalancer/adding-ingress.md#adding-certificates-to-the-ingress) — Attach multiple TLS certs to AWS LB Ingress.¹<sup>,</sup>²
* AWS - Amazon Linux 2023 support.¹<sup>,</sup>²
* Azure - [MSSQL Backup retention](../../overview-2/azure-services/databases/sql-database.md#updating-the-backup-retention-period-for-a-database) — Enable and manage Azure SQL Server backup retention.¹
* Azure - [Deleted Key Vaults listing](../overview-2/azure-services/key-vault.md#managing-deleted-azure-key-vaults) — View and recover or purge deleted Azure Key Vaults.¹
* Azure - [Azure CosmosDB support](../overview-2/azure-services/databases/cosmosdb.md) — Provision and manage CosmosDB resources in Azure.¹
* GCP - [Cloud SQL edition attribute](../overview-1/gcp-services/gcp-databases/cloud-sql.md#creating-a-cloud-sql-database) — Add and manage edition attributes for Cloud SQL instances.¹
* GCP - [Ingress TLS annotation support](../kubernetes-overview/ingress-loadbalancer/gke-ingress.md#configuring-the-ingress) — Use annotations to configure TLS host and secret.¹
* GCP - [PostgreSQL dedicated node types](../overview-1/gcp-services/gcp-databases/cloud-sql.md#creating-a-cloud-sql-database) — Use dedicated nodes for PostgreSQL deployments.¹
* GCP - [Disable NAT during infra creation](../../overview-1/use-cases/creating-an-infrastructure-and-plan-for-gcp/) — Option to skip NAT setup when creating infra.¹
* GCP - [GCP Secret Manager support](../overview-1/gcp-services/gcp-secrets-manager.md) — Manage secrets using GCP Secret Manager service.¹
* GCP - [Firewall rule support](../overview-1/security-configuration-settings/gcp-firewall-rules/) — Manage network rules at the infrastructure and tenant levels.¹
* GCP - [Security Command Center](../overview-1/gcp-services/gcp-security-command-center.md) — Integration with GCP Security Command Center.¹
* GCP - [Standalone SSL certificates](../overview-1/prerequisites/create-managed-ssl-certificates-for-gcp.md) — Support for GCP Certificate Manager SSL certs.¹
* Kubernetes - [Argo Workflows](../introduction-to-ci-cd/argo-workflows.md) — Run and manage Kubernetes-native workflows.¹<sup>,</sup>²
* Kubernetes - [Group and view services by App](../overview/aws-services/containers/eks-containers-and-services/#id-7-toc-title) — Organize Kubernetes services by App Name.¹<sup>,</sup>²
* Kubernetes - [K8s secrets & ConfigMaps backup](../kubernetes-overview/configs-and-secrets/backing-up-and-restoring-kubernetes-secrets-and-configmaps.md) — Backups for K8s secrets and ConfigMaps.¹
* Kubernetes - [Helm Repo with OCI support](../kubernetes-overview/helm/oci-helm-repositories.md) — Support OCI-compliant Helm registries.¹
* Kubernetes - [HelmRelease with `ValuesFrom`](../kubernetes-overview/helm/helm-charts.md) — Pull Helm chart values from external sources.¹
* Identity/Access Management - [PermissionSets user groups](../security-and-compliance/access-control-2/permission-sets.md#creating-a-user-group) — Apply PermissionSets to groups.²
* Cost Management - [Billing Alerts](../diagnostics-overview/configure-billing-alerts.md) — Configure billing alerts across AWS, Azure, and GCP.¹
* Identity/Access Management – [PermissionSet RBAC](../security-and-compliance/access-control-2/permission-sets.md#configuring-permission-sets-in-duplocloud) — Priority-based role evaluation.¹
* AWS - [EKS Taint Support](../overview/aws-services/containers/eks-containers-and-services/#creating-a-duplocloud-eks-service) — Support adding taints to EKS nodes after node creation.¹
* AWS - [Tenant Security Group IPv6](../../security-and-compliance/access-control/security-groups.md) — Support IPv6 rules in Tenant-level security groups.¹
* AWS - [External DNS Infra Setting](../overview/aws-systems-settings/aws-infrastructure-settings.md#infrastructure-settings) for managing DNS record behavior.¹
* AWS - [Amazon CloudFront](../overview/aws-services/cloudfront/cloudfront.md) — Support for CloudFront distributions through DuploCloud.¹
* GCP - Support for defining [GCP Maintenance Windows](../overview-1/use-cases/gke-maintenance-windows.md).¹
* GCP - Support for [GCP Cloud Run Service](../overview-1/gcp-services/cloud-run-service.md).¹
* GCP - Support for [dynamic NAT port allocation](../overview-1/gcp-services/dynamic-nat-port-allocation.md) during GCP infrastructure creation.¹
* GCP - Support for [Cloud Tasks](../overview-1/gcp-services/gcp-cloud-task-support.md) integration.²
* Azure - Support for managing [infra secrets in Azure](../overview-2/azure-services/infra-secrets.md).¹
* Kubernetes - [Cron Job Recent Job Link](../../kubernetes/cronjobs.md) — Navigate from a CronJob to most recent execution.¹<sup>,</sup>²
* Kubernetes - [ArgoCD integration](../introduction-to-ci-cd/argocd.md) — Support for GitOps deployment and management workflows.¹
* Kubernetes - [ResourceQuota](../kubernetes-overview/resourcequotas.md) — Manage namespace resource limits.¹
* Notifications - [Custom Alert Emails](../access-control/user-access-and-permissions/user-email-notifications.md) — Manage custom email addresses for alert notifications.²
* IaC - [Pulumi integration support ](../pulumi-user-guide/)for managing DuploCloud infrastructure as code.¹
* Observability - Usability improvements/Flame Graph feature in [Advanced Observability Suite](../diagnostics-overview/advanced-observability-suite/).¹
* Networking - [Ignore DNS record prefixes](../duplocloud-prerequisites/resolving-dns-failures.md#configuring-duplocloud-to-ignore-dns-entries) to safely add custom entries.¹
* User Administration - [Customization for welcome emails](../access-control/user-access-and-permissions/user-email-notifications.md#customizing-welcome-emails-for-new-users) sent to new users.¹
* User Administration - [Automatic email alerts when new Admin users are added.](../access-control/user-access-and-permissions/user-email-notifications.md#configuring-new-admin-user-email-notifications)²
* Security & Compliance - [Customizable Kibana URL for Audit Logs.](../diagnostics-overview/standard-observability-suite/setup/auditing/custom-kibana-audit-url.md)²
* Observability - [Customizable Kibana URL for Logging Views.](../diagnostics-overview/standard-observability-suite/setup/logging-setup/custom-kibana-logging-url.md)²
* AWS - Create and manage [Target Groups for EC2 Instances, IPs, and ALBs (AWS)](../overview/aws-services/load-balancers/target-groups.md).¹
* AWS - Support for [ElastiCache Valkey](../overview/aws-services/database/elastic-cache.md#creating-a-redis-or-valkey-elasticache-instance).¹
* AWS - [Set Retry and Expiration Limits for Asynchronous Lambda Invocations.](../../overview/aws-services/lambda/)¹
* AWS - Configure [SQS dead letter queues and redrive policies in AWS](../overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/instance-refresh-for-asg.md).¹
* AWS - Support for Modifying [ASG Launch Templates](../overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/launch-templates.md).¹
* AWS - [Instance Refresh action for AWS Auto Scaling Groups (ASG)](../overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/instance-refresh-for-asg.md).¹
* AWS - Customize CloudWatch metrics for [AWS Auto Scaling Groups (ASG)](../overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/#creating-autoscaling-groups-asg).¹
* AWS - [SNS with FIFO (First-In-First-Out) topics.](../overview/aws-services/sns-topic.md#creating-a-sns-topic)¹
* AWS - Create scheduled snapshot windows for automated backups in [AWS Redis](../overview-2/azure-services/databases/redis-database.md).¹
* AWS - Support for [taints with EKS Hosts or Agent Pools](../../overview/use-cases/hosts-vms/display-tainted-ec2-hosts.md).¹<sup>,</sup>²
* AWS - [Download inventory reports of all AWS resources](../../extras-overview/inventory.md#downloading-an-inventory-report) (for StateRAMP compliance).¹
* AWS - Support for [Lambda JAR with S3](../../overview/aws-services/lambda/#id-3-toc-title).¹
* AWS - Support for aurora-iopt1 storage type in [Aurora RDS](../../aws-user-guide/aws-services/database/rds-database/#id-0-toc-title).¹
* AWS - Force delete and update settings options added for [ECR repositories](../overview/aws-services/elastic-container-registry-ecr/#updating-ecr-repository-settings).¹
* AWS - Support for [serverless Kafka clusters](../overview/aws-services/kafka-cluster.md#creating-a-kafka-cluster) for AWS users.¹
* AWS - [Disable AWS JIT access for non-admin users](../overview/use-cases/jit-access.md#disabling-jit-access-for-non-admin-users).¹
* AWS - Support for configuring [S3 bucket replication rules](https://app.gitbook.com/o/ojpRPRrP7bqrzOUuLmOz/s/68cb0s9ce5UIUKWPuYs8/~/changes/1184/overview/aws-services/s3-bucket/~/overview#s3-bucket-replication-rules).¹
* AWS - Update [RDS Performance Insights](../../aws-user-guide/aws-services/database/rds-database/#updating-performance-insights-for-an-existing-rds).¹
* AWS - Update [ECR repository settings](../overview/aws-services/elastic-container-registry-ecr/).¹&#x20;
* AWS - [Enable delete protection for AWS Load Balancers.](../overview/aws-services/load-balancers/#additional-load-balancer-settings)¹&#x20;
* AWS - Support for adding TLS Hosts and TLS Secrets fields when configuring[ Ingress for EKS](../../kubernetes-overview/ingress-loadbalancer/adding-ingress.md).¹
* AWS - Automatically redirect incoming HTTP requests to HTTPS for [EKS Ingress](../../kubernetes-overview/ingress-loadbalancer/adding-ingress.md).¹
* AWS - Support for [ECS with EC2 Capacity Provider](../../overview/aws-services/containers/ecs-containers-and-task-definitions/#configuring-ecs-with-ec2-capacity-provider).²
* Azure - Add new secret versions in [Azure Key Vault](../overview-2/azure-services/key-vault.md).²
* Azure - Support for [Azure Container Registry](../../overview-2/azure-services/azure-container-registry-acr.md).²
* Azure - Support for [Azure Availability Sets](../overview-2/use-cases/hosts-vms/availability-sets.md).¹
* Azure - Support for [Azure Data Factory](../overview-2/azure-services/data-factory.md).¹
* Azure - [Enable autoscaling in the AKS default node pool](../overview-2/use-cases/infrastructure-and-plan/aks-initial-setup.md).¹
* Azure - Automatically redirect incoming HTTP requests to HTTPS for [AKS Ingress](../kubernetes-overview/ingress-loadbalancer/aks-ingress/).¹
* GCP - Enable automation to [retain backups when a Cloud SQL instance is deleted](../overview-1/gcp-services/gcp-databases/cloud-sql.md#retaining-backups-before-cloud-sql-deletion).¹
* GCP - Support for [GCP Virtual Private Cloud (VPC) Peering](../overview-1/gcp-services/virtual-private-cloud-vpc-peering.md).¹
* GCP - Support for [SNS Pub/Sub topic subscriptions](../overview-1/gcp-services/s3-bucket-3.md#create-a-pub-sub-topic-subscription).¹
* Kubernetes - Support for Jobs and CronJobs on [Shared Hosts in AWS](../overview/use-cases/hosts-vms/adding-shared-hosts.md#creating-a-job-or-cronjob-to-run-on-a-shared-host) and [Shared VMs in Azure](../overview/use-cases/hosts-vms/adding-shared-hosts.md#creating-a-job-or-cronjob-to-run-on-a-shared-host).¹
* Kubernetes - [Manage read-only access to Kubernetes Secrets and ConfigMaps.](../kubernetes-overview/configs-and-secrets/managing-secret-access-for-read-only-users-aws-and-gcp.md)¹
* Kubernetes - Add custom Kubernetes labels to nodes in AWS ([host](../overview/use-cases/hosts-vms/) or [Auto Scaling Group](../overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/) (ASG).¹
* Kubernetes - Support for [initContainers and additionalContainers (Sidecar Containers)](../kubernetes-overview/initcontainers-and-sidecar-containers.md).¹
* Identity/Access Management - [Support for granular access control with new Permission Sets.](../security-and-compliance/access-control-2/permission-sets.md)²
* Kubernetes- Support for [rolling back container images](../overview/aws-services/containers/container-rollback.md) for DuploCloud Services.¹
* Identity/Access Management - [Manage automatic VPN access for new Okta users.](../access-control/user-access-and-permissions/add-and-delete-vpn-access-for-users.md#managing-vpn-access-for-okta-users)¹
* Identity/Access Management - [Force sync Okta changes](/broken/pages/yeRYLkYWOI0ef3Tgwdd6) to immediately apply updates.¹
* UX - UI redesign: updates to navigation, breadcrumbs, menus, and general appearance.¹
* User Administration - [Configure session timeout duration for user logins.](../access-control/api-and-session-management/session-timeout.md#configuring-session-timeout-for-duplocloud-users)¹

**Release Key**\
¹ Available from January 2025 release\
² Available from November 2025 release\
¹<sup>,</sup>² Available as part of January and November 2025 releases

To view earlier updates, see the [Archives](product-update-archives.md).
