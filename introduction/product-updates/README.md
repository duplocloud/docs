---
description: New features and enhancements in DuploCloud
cover: ../../.gitbook/assets/Linkedin-bannerV3 (1) (1).png
coverY: 0
---

# Product Updates

_**Last Updated, January 6, 2026**_

* AWS - [ECS Run Task](../../automation-platform/overview/aws-services/containers/ecs-containers-and-task-definitions/#running-a-task-optional) — Allow selecting a capacity provider strategy when running ECS tasks.
* AWS - [S3 Event Notifications](../../automation-platform/overview/aws-services/s3-bucket/s3-bucket-notifications.md) — Support for configuring Amazon S3 event notifications.
* AWS - [Lambda Edit Menu Updates](../../overview/aws-services/lambda/#id-3-toc-title) — Add Maximum Retry Attempts and Maximum Event Age.
* Kubernetes - Suspend [CronJobs](../../kubernetes/cronjobs.md#suspending-a-cronjob) using a suspend true/false setting.
* General - Attach a default [Web Application Firewall (WAF)](../../automation-platform/overview/aws-services/web-application-firewall-waf.md#attaching-the-waf-to-a-load-balancer) to all ALBs at the tenant level.
* General - [Tenant Indicator](../../automation-platform/access-control/setting-tenant-topbar-color.md) — Customize the top bar color for individual tenants.
* General - [AI Slack Integration](../../ai-suite/ai-helpdesk/) — Support for integrating DuploCloud AI capabilities with Slack.
* AWS - [CloudFront Origin Access Control](../../aws-user-guide/aws-services/cloudfront.md) — Use OAC instead of deprecated OAI.
* AWS - [EKS AutoMode](../../automation-platform/overview/use-cases/eks-auto-mode.md) — Automatically configure node scaling and management for EKS clusters.
* General - [Okta Management](../../automation-platform/access-control/sso-configuration/okta-management-settings.md) — Configure Okta authentication settings directly in DuploCloud.
* AWS - [ECS ASG sharing](../../automation-platform/overview/aws-services/containers/ecs-containers-and-task-definitions/sharing-ec2-auto-scaling-groups-across-tenants-for-ecs.md) — Sharing EC2 Auto Scaling Groups across tenants for ECS.
* AWS - [KMS key management](../../automation-platform/security-and-compliance/access-control-1/at-rest-encryption/kms-keys.md) — Manage AWS KMS keys at the tenant level in DuploCloud.
* AWS - [ElastiCache global datastore](../../automation-platform/overview/aws-services/database/elastic-cache.md#creating-a-global-datastore) — Support for global ElastiCache clusters.
* AWS - [AMI enhancements](../../automation-platform/overview/use-cases/hosts-vms/create-amazon-machine-image-ami.md) — Select, restrict, or share AMIs across Tenants.
* AWS - [Amazon MQ support](../../automation-platform/overview/aws-services/amazon-mq.md) — Provision and manage AWS MQ brokers in DuploCloud.
* AWS - [App Runner support](../../automation-platform/overview/aws-services/app-runner.md) — Provision and manage AWS App Runner services.
* AWS - [ECS launch and network mode](../../automation-platform/overview/aws-services/containers/ecs-containers-and-task-definitions/#creating-a-task-definition) — Select launch type and network mode for ECS tasks.
* AWS - [OpenSearch upgrade support](../../automation-platform/overview/aws-services/elasticsearch.md#managing-an-opensearch-instance) — Upgrade OpenSearch versions within DuploCloud.
* AWS - [EC2 Snapshots](../../automation-platform/overview/use-cases/hosts-vms/ec2-snapshots.md) — Support for managing and automating EC2 volume snapshots.
* AWS - [Ingress: Multi-certificate support](../../kubernetes-overview/ingress-loadbalancer/adding-ingress.md#adding-certificates-to-the-ingress) — Attach multiple TLS certs to AWS LB Ingress.
* Azure - [MSSQL Backup retention](../../automation-platform/overview-2/azure-services/databases/sql-database.md#updating-the-backup-retention-period-for-a-database) — Enable and manage backup retention for Azure SQL Server.
* Azure - [Deleted Key Vaults listing](../../automation-platform/overview-2/azure-services/key-vault.md#managing-deleted-azure-key-vaults) — View and recover or purge deleted Azure Key Vaults.
* Azure - [Azure CosmosDB support](../../automation-platform/overview-2/azure-services/databases/cosmosdb.md) — Provision and manage CosmosDB resources in Azure.
* GCP - [Cloud SQL edition attribute](../../automation-platform/overview-1/gcp-services/gcp-databases/cloud-sql.md#creating-a-cloud-sql-database) — Add and manage edition attributes for Cloud SQL instances.
* GCP - [Ingress TLS annotation support](../../automation-platform/kubernetes-overview/ingress-loadbalancer/gke-ingress.md#configuring-the-ingress) — Use annotations to configure TLS host and secret.
* GCP - [PostgreSQL dedicated node types](../../automation-platform/overview-1/gcp-services/gcp-databases/cloud-sql.md#creating-a-cloud-sql-database) — Use dedicated nodes for PostgreSQL deployments.
* GCP - [Disable NAT during infra creation](../../automation-platform/overview-1/use-cases/creating-an-infrastructure-and-plan-for-gcp/) — Option to skip NAT setup when creating infra.
* GCP - [GCP Secret Manager support](../../automation-platform/overview-1/gcp-services/gcp-secrets-manager.md) — Manage secrets using GCP Secret Manager service.
* GCP - [Firewall rule support](../../automation-platform/overview-1/security-configuration-settings/gcp-firewall-rules/) — Manage network rules at the infrastructure and tenant levels.
* GCP - [Security Command Center](../../automation-platform/overview-1/gcp-services/gcp-security-command-center.md) — Integration with GCP Security Command Center.
* GCP - [Standalone SSL certificates](../../automation-platform/overview-1/prerequisites/create-managed-ssl-certificates-for-gcp.md) — Support for GCP Certificate Manager SSL certs.
* Kubernetes - [Argo Workflows](../../automation-platform/introduction-to-ci-cd/argo-workflows.md) — Run and manage Kubernetes-native workflows.
* Kubernetes - [Group and view services by App](../../automation-platform/overview/aws-services/containers/eks-containers-and-services/#id-7-toc-title) — Organize Kubernetes services by  App Name.
* Kubernetes - [K8s secrets & ConfigMaps backup](../../automation-platform/kubernetes-overview/configs-and-secrets/backing-up-and-restoring-kubernetes-secrets-and-configmaps.md) — Backups for K8s secrets and ConfigMaps.
* Kubernetes - [Helm Repo with OCI support](../../automation-platform/kubernetes-overview/helm/oci-helm-repositories.md) — Support OCI-compliant Helm registries.
* Kubernetes - [HelmRelease with `ValuesFrom`](../../automation-platform/kubernetes-overview/helm/helm-charts.md) — Pull Helm chart values from external sources.
* General - [User groups in PermissionSets](../../automation-platform/security-and-compliance/access-control-2/permission-sets.md#creating-a-user-group) — Apply PermissionSets to user groups for simplified access control.
* General - [Billing Alerts](../../automation-platform/diagnostics-overview/configure-billing-alerts.md) — Configure billing alerts across AWS, Azure, and GCP.
* General - [PermissionSet RBAC enhancements](../../automation-platform/security-and-compliance/access-control-2/permission-sets.md) — Support priority-based and advanced role evaluation.
* AWS - [EKS Taint Support](../../automation-platform/overview/aws-services/containers/eks-containers-and-services/#creating-a-duplocloud-eks-service) — Support adding taints to EKS nodes after node creation.
* AWS - [Tenant Security Group IPv6](../../security-and-compliance/access-control/security-groups.md) — Support IPv6 rules in tenant-level security groups.
* AWS - [External DNS Infra Setting](../../automation-platform/overview/aws-systems-settings/aws-infrastructure-settings.md#infrastructure-settings) for managing DNS record behavior.
* AWS - [Amazon CloudFront](../../aws-user-guide/aws-services/cloudfront.md) — Support for CloudFront distributions through DuploCloud.
* GCP - Support for defining [GCP Maintenance Windows](../../automation-platform/overview-1/use-cases/gke-maintenance-windows.md).
* GCP - Support for [GCP Cloud Run Service](../../automation-platform/overview-1/gcp-services/cloud-run-service.md).
* GCP - Support for [dynamic NAT port allocation](../../automation-platform/overview-1/gcp-services/dynamic-nat-port-allocation.md) during GCP infrastructure creation.
* GCP - Support for [Cloud Tasks](../../automation-platform/overview-1/gcp-services/gcp-cloud-task-support.md) integration.
* Azure - Support for managing [infra secrets in Azure](../../automation-platform/overview-2/azure-services/infra-secrets.md).
* Kubernetes - [Cron Job Recent Job Link](../../kubernetes/cronjobs.md) — Navigate from a CronJob to its most recent execution.
* Kubernetes - [ArgoCD integration](../../automation-platform/introduction-to-ci-cd/argocd.md) — Support for GitOps deployment and management workflows.
* Kubernetes - [ResourceQuota](../../automation-platform/kubernetes-overview/resourcequotas.md) — Manage namespace resource limits.
* General - [Custom Alert Emails](../../automation-platform/access-control/user-email-notifications.md) — Add and manage custom email addresses for alert notifications.
* General - [Pulumi integration support ](../../automation-platform/pulumi-user-guide/)for managing DuploCloud infrastructure as code.
* General - Usability improvements and a new Explain Flame Graph feature were added to [DuploCloud Advanced Observability Suite](../../automation-platform/diagnostics-overview/advanced-observability-suite/).
* General - Configure DuploCloud to [ignore DNS record prefixes](../../automation-platform/duplocloud-prerequisites/resolving-dns-failures.md#configuring-duplocloud-to-ignore-dns-entries), allowing you to safely add custom entries without risk of deletion.
* General - [Customization for welcome emails](../../automation-platform/access-control/user-email-notifications.md#customizing-welcome-emails-for-new-users) sent to new users upon account creation.
* General - [Automatic email alerts when new Admin users are added.](../../automation-platform/access-control/user-email-notifications.md#configuring-new-admin-user-email-notifications)
* General - [Customizable Kibana URL for Audit Logs.](../../automation-platform/diagnostics-overview/standard-observability-suite/setup/auditing/custom-kibana-audit-url.md)
* General - [Customizable Kibana URL for Logging Views.](../../automation-platform/diagnostics-overview/standard-observability-suite/setup/logging-setup/custom-kibana-logging-url.md)
* AWS - Create and manage [Target Groups for EC2 Instances, IPs, and ALB Load Balancers (AWS)](../../automation-platform/overview/aws-services/load-balancers/target-groups.md).
* AWS - Support for [ElastiCache Valkey](../../automation-platform/overview/aws-services/database/elastic-cache.md#creating-a-redis-or-valkey-elasticache-instance).
* AWS - Set Retry and Expiration Limits for Asynchronous [Lambda](../../overview/aws-services/lambda/) Invocations.
* AWS - Configure [SQS dead letter queues and redrive policies in AWS](../../automation-platform/overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/instance-refresh-for-asg.md).
* AWS - Support for Modifying [ASG Launch Templates](../../automation-platform/overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/launch-templates.md).
* AWS - [Instance Refresh action for AWS Auto Scaling Groups (ASG)](../../automation-platform/overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/instance-refresh-for-asg.md).
* AWS - Customize CloudWatch metrics for [AWS Auto Scaling Groups (ASG)](../../automation-platform/overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/#creating-autoscaling-groups-asg).
* AWS - Support for [SNS with FIFO (First-In-First-Out) topics.](../../automation-platform/overview/aws-services/sns-topic.md#creating-a-sns-topic)
* AWS - Create scheduled snapshot windows for automated backups in [AWS Redis](../../automation-platform/overview-2/azure-services/databases/redis-database.md).
* AWS - Support for [taints with EKS Hosts or Agent Pools](../../overview/use-cases/hosts-vms/display-tainted-ec2-hosts.md).
* AWS - [Download inventory reports of all AWS resources](../../extras-overview/inventory.md#downloading-an-inventory-report) (for StateRAMP compliance).
* AWS - Support for [Lambda JAR with S3](../../overview/aws-services/lambda/#id-3-toc-title).
* AWS - Support for aurora-iopt1 storage type in [Aurora RDS](../../aws-user-guide/aws-services/database/rds-database/#id-0-toc-title).
* AWS - Force delete and update settings options added for [ECR repositories](../../automation-platform/overview/aws-services/elastic-container-registry-ecr/#updating-ecr-repository-settings).&#x20;
* AWS - Select and update [Certificate Authorities for RDS instances](../../aws-user-guide/aws-services/database/rds-database/#managing-rds-certificate-authorities).
* AWS - Specify an initial database during [RDS instance creation](../../aws-user-guide/aws-services/database/rds-database/#id-0-toc-title).
* AWS - Support for [serverless Kafka clusters](../../automation-platform/overview/aws-services/kafka-cluster.md#creating-a-kafka-cluster) for AWS users.
* AWS - [Disable AWS JIT access for non-admin users](../../automation-platform/overview/use-cases/jit-access.md#disabling-jit-access-for-non-admin-users).
* AWS - Support for configuring [S3 bucket replication rules](https://app.gitbook.com/o/ojpRPRrP7bqrzOUuLmOz/s/68cb0s9ce5UIUKWPuYs8/~/changes/1184/overview/aws-services/s3-bucket/~/overview#s3-bucket-replication-rules).
* AWS - Update [RDS Performance Insights](../../aws-user-guide/aws-services/database/rds-database/#updating-performance-insights-for-an-existing-rds).
* AWS - Update [ECR repository settings](../../automation-platform/overview/aws-services/elastic-container-registry-ecr/).&#x20;
* AWS - [Enable delete protection for AWS Load Balancers.](../../automation-platform/overview/aws-services/load-balancers/#additional-load-balancer-settings)
* AWS - Support for adding TLS Hosts and TLS Secrets fields when configuring an[ Ingress for EKS](../../kubernetes-overview/ingress-loadbalancer/adding-ingress.md).
* AWS - Automatically redirect incoming HTTP requests to HTTPS for [EKS Ingress](../../kubernetes-overview/ingress-loadbalancer/adding-ingress.md).&#x20;
* AWS - Support for [ECS with EC2 Capacity Provider](../../automation-platform/overview/aws-services/containers/ecs-containers-and-task-definitions/#configuring-ecs-with-ec2-capacity-provider).
* Azure - Add new secret versions in [Azure Key Vault](../../automation-platform/overview-2/azure-services/key-vault.md).
* Azure - Support for [Azure Databricks](../../automation-platform/overview-2/azure-services/databricks.md).
* Azure - Support for [Azure Container Registry](../../automation-platform/overview-2/azure-services/azure-container-registry-acr.md).
* Azure - Support for [Azure Availability Sets](../../automation-platform/overview-2/use-cases/hosts-vms/availability-sets.md).
* Azure - Support for [Azure Data Factory](../../automation-platform/overview-2/azure-services/data-factory.md).&#x20;
* Azure - [Enable autoscaling in the AKS default node pool](../../automation-platform/overview-2/use-cases/infrastructure-and-plan/aks-initial-setup.md).
* Azure - Automatically redirect incoming HTTP requests to HTTPS for [AKS Ingress](../../automation-platform/kubernetes-overview/ingress-loadbalancer/aks-ingress/).
* GCP - Enable automation to [retain backups when a Cloud SQL instance is deleted](../../automation-platform/overview-1/gcp-services/gcp-databases/cloud-sql.md#retaining-backups-before-cloud-sql-deletion).
* GCP - Support for [GCP Virtual Private Cloud (VPC) Peering](../../automation-platform/overview-1/gcp-services/virtual-private-cloud-vpc-peering.md).
* GCP - Support for [SNS Pub/Sub topic subscriptions](../../automation-platform/overview-1/gcp-services/s3-bucket-3.md#create-a-pub-sub-topic-subscription).
* Kubernetes - Support for Jobs and CronJobs on [Shared Hosts in AWS](../../automation-platform/overview/use-cases/hosts-vms/adding-shared-hosts.md#creating-a-job-or-cronjob-to-run-on-a-shared-host) and [Shared VMs in Azure](../../automation-platform/overview/use-cases/hosts-vms/adding-shared-hosts.md#creating-a-job-or-cronjob-to-run-on-a-shared-host).
* Kubernetes - [Manage read-only access to Kubernetes Secrets and ConfigMaps.](../../automation-platform/kubernetes-overview/configs-and-secrets/managing-secret-access-for-read-only-users-aws-and-gcp.md)
* Kubernetes - Add custom Kubernetes labels to nodes in AWS ([host](../../automation-platform/overview/use-cases/hosts-vms/) or [Auto Scaling Group](../../automation-platform/overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/) (ASG).
* Kubernetes - Support for [initContainers and additionalContainers (Sidecar Containers)](../../automation-platform/kubernetes-overview/initcontainers-and-sidecar-containers.md).
* General - [Support for granular access control with new Permission Sets.](../../automation-platform/security-and-compliance/access-control-2/permission-sets.md)
* General - Support for [rolling back container images](../../automation-platform/overview/aws-services/containers/container-rollback.md) for DuploCloud Services.
* General - [Manage automatic VPN access for new Okta users. ](../../automation-platform/access-control/add-and-delete-vpn-access-for-users.md#managing-vpn-access-for-okta-users)
* General - Force sync [Okta](../../automation-platform/access-control/sso-configuration/okta-identity-management.md) changes to immediately apply updates.
* General - UI redesign: updates to navigation, breadcrumbs, menus, and general appearance.
* General - [Configure session timeout duration for user logins.](../../automation-platform/access-control/session-timeout.md#configuring-session-timeout-for-duplocloud-users)

To view earlier updates, see the [Archives](product-update-archives.md).
