---
description: New features and enhancements in DuploCloud
cover: ../.gitbook/assets/banner dark.png
coverY: 0
---

# Product Updates

## Q4 2025

AWS

* [CloudFront Origin Access Control](../aws-user-guide/aws-services/cloudfront.md) — Use OAC instead of deprecated OAI for new distributions, with automatic permission management.
* [EKS AutoMode](../automation-platform/overview/use-cases/eks-auto-mode.md) — Automatically configure node scaling and management for EKS clusters.

General

* [Okta Management](../automation-platform/access-control/sso-configuration/okta-management-settings.md) — Configure and manage Okta authentication settings directly in DuploCloud.

## Q3 2025

AWS

* [ECS ASG sharing](../automation-platform/overview/aws-services/containers/ecs-containers-and-task-definitions/sharing-ec2-auto-scaling-groups-across-tenants-for-ecs.md) — Sharing EC2 Auto Scaling Groups across tenants for ECS.
* [KMS key management](../automation-platform/security-and-compliance/access-control-1/at-rest-encryption/kms-keys.md) — Manage AWS KMS keys at the tenant level in DuploCloud.
* [ElastiCache global datastore](../automation-platform/overview/aws-services/database/elastic-cache.md#creating-a-global-datastore) — Support for provisioning and managing global ElastiCache clusters.
* [AMI enhancements](../automation-platform/overview/use-cases/hosts-vms/create-amazon-machine-image-ami.md) — Select, restrict, or share AMIs across Tenants.
* [Amazon MQ support](../automation-platform/overview/aws-services/amazon-mq.md) — Provision and manage AWS MQ brokers in DuploCloud.
* [App Runner support](../automation-platform/overview/aws-services/app-runner.md) — Provision and manage AWS App Runner services.
* [ECS launch and network mode](../automation-platform/overview/aws-services/containers/ecs-containers-and-task-definitions/#creating-a-task-definition) — Select launch type and network mode for ECS tasks.
* [OpenSearch upgrade support](../automation-platform/overview/aws-services/elasticsearch.md#managing-an-opensearch-instance) — Upgrade OpenSearch versions within DuploCloud.
* [EC2 Snapshots](../automation-platform/overview/use-cases/hosts-vms/ec2-snapshots.md) — Support for managing and automating EC2 volume snapshots.
* [Ingress: Multi-certificate support](../kubernetes-overview/ingress-loadbalancer/adding-ingress.md#adding-certificates-to-the-ingress) — Attach multiple TLS certs to AWS LB–managed Ingress.

Azure

* [MSSQL Backup retention](../automation-platform/overview-2/azure-services/databases/sql-database.md#updating-the-backup-retention-period-for-a-database) — Enable and manage backup retention for Azure SQL Server.
* [Deleted Key Vaults listing](../automation-platform/overview-2/azure-services/key-vault.md#managing-deleted-azure-key-vaults) — View and recover or purge deleted Azure Key Vaults.
* [Azure CosmosDB support](../automation-platform/overview-2/azure-services/databases/cosmosdb.md) — Provision and manage CosmosDB resources in Azure.

GCP

* [Cloud SQL edition attribute](../automation-platform/overview-1/gcp-services/gcp-databases/cloud-sql.md#creating-a-cloud-sql-database) — Add and manage edition attributes for Cloud SQL instances.
* [Ingress TLS annotation support](../automation-platform/kubernetes-overview/ingress-loadbalancer/gke-ingress.md#configuring-the-ingress) — Use annotations to configure TLS host and secret.
* [PostgreSQL dedicated node types](../automation-platform/overview-1/gcp-services/gcp-databases/cloud-sql.md#creating-a-cloud-sql-database) — Use dedicated nodes for PostgreSQL deployments.
* [Disable NAT during infra creation](../automation-platform/overview-1/use-cases/creating-an-infrastructure-and-plan-for-gcp/) — Option to skip NAT setup when creating infra.
* [GCP Secret Manager support](../automation-platform/overview-1/gcp-services/gcp-secrets-manager.md) — Manage secrets using GCP Secret Manager service.
* [Firewall rule support](../automation-platform/overview-1/security-configuration-settings/gcp-firewall-rules/) — Define and manage network rules at the infrastructure and tenant levels.
* [Security Command Center](../automation-platform/overview-1/gcp-services/gcp-security-command-center.md) — Integration with GCP Security Command Center.
* [Standalone SSL certificates](../automation-platform/overview-1/prerequisites/create-managed-ssl-certificates-for-gcp.md) — Support for GCP Certificate Manager SSL certs.

Kubernetes

* [Argo Workflows](../automation-platform/introduction-to-ci-cd/argo-workflows.md) — Run and manage Kubernetes-native workflows.
* [Group and view services by App](../automation-platform/overview/aws-services/containers/eks-containers-and-services/#id-7-toc-title) — Organize Kubernetes services by  App Name.
* [K8s secrets & ConfigMaps backup](../automation-platform/kubernetes-overview/configs-and-secrets/backing-up-and-restoring-kubernetes-secrets-and-configmaps.md) — Manage backups for K8s secrets and ConfigMaps.
* [Helm Repo with OCI support](../automation-platform/kubernetes-overview/helm/oci-helm-repositories.md) — Support for adding Helm repositories from OCI-compliant registries.
* [HelmRelease with `ValuesFrom`](../automation-platform/kubernetes-overview/helm/helm-charts.md) — Pull Helm chart values from external sources.

General

* [User groups in PermissionSets](../automation-platform/security-and-compliance/access-control-2/permission-sets.md#creating-a-user-group) — Apply PermissionSets to user groups for simplified access control.
* [Billing Alerts](../automation-platform/diagnostics-overview/configure-billing-alerts.md) — Configure billing alerts across AWS, Azure, and GCP.
* [PermissionSet RBAC enhancements](../automation-platform/security-and-compliance/access-control-2/permission-sets.md) — Support priority-based and advanced role evaluation.

## Q2 2025

* AWS
  * [Tenant Security Group IPv6](../security-and-compliance/access-control/security-groups.md) — Support IPv6 rules in tenant-level security groups.
  * [External DNS Infra Setting](../automation-platform/overview/aws-systems-settings/aws-infrastructure-settings.md#infrastructure-settings) for managing DNS record behavior.
  * Support for managing [Amazon CloudFront](../aws-user-guide/aws-services/cloudfront.md) distributions through DuploCloud.
* GCP
  * Support for defining [GCP Maintenance Windows](../automation-platform/overview-1/use-cases/gke-maintenance-windows.md).
  * Support for [GCP Cloud Run Service](../automation-platform/overview-1/gcp-services/cloud-run-service.md).
  * Support for [dynamic NAT port allocation](../automation-platform/overview-1/gcp-services/dynamic-nat-port-allocation.md) during GCP infrastructure creation.
  * Support for [Cloud Tasks](../automation-platform/overview-1/gcp-services/gcp-cloud-task-support.md) integration.
* Azure
  * Support for managing [infra secrets in Azure](../automation-platform/overview-2/azure-services/infra-secrets.md).
* Kubernetes
  * [Cron Job Recent Job Link](../kubernetes/cronjobs.md) — Quickly navigate from a CronJob to its most recent execution.
  * Support for [ArgoCD integration](../automation-platform/introduction-to-ci-cd/argocd.md), enabling GitOps deployment and management workflows within DuploCloud.
  * Support for [ResourceQuota](../automation-platform/kubernetes-overview/resourcequotas.md) to manage namespace resource limits.
* General
  * [Custom Alert Emails](../automation-platform/access-control/user-email-notifications.md) — Add and manage custom email addresses for alert notifications.
  * [Pulumi integration support ](../automation-platform/pulumi-user-guide/)for managing DuploCloud infrastructure as code.
  * Usability improvements and a new Explain Flame Graph feature were added to [DuploCloud Advanced Observability Suite](../automation-platform/diagnostics-overview/advanced-observability-suite/).
  * Configure DuploCloud to [ignore DNS record prefixes](../automation-platform/duplocloud-prerequisites/resolving-dns-failures.md#configuring-duplocloud-to-ignore-dns-entries), allowing you to safely add custom entries without risk of deletion.
  * [Customization for welcome emails](../automation-platform/access-control/user-email-notifications.md#customizing-welcome-emails-for-new-users) sent to new users upon account creation.
  * [Automatic email alerts when new Admin users are added.](../automation-platform/access-control/user-email-notifications.md#configuring-new-admin-user-email-notifications)
  * [Customizable Kibana URL for Audit Logs.](../automation-platform/diagnostics-overview/standard-observability-suite/setup/auditing/custom-kibana-audit-url.md)
  * [Customizable Kibana URL for Logging Views.](../automation-platform/diagnostics-overview/standard-observability-suite/setup/logging-setup/custom-kibana-logging-url.md)

## Q1 2025

* AWS
  * Create and manage [Target Groups for EC2 Instances, IPs, and ALB Load Balancers (AWS)](../automation-platform/overview/aws-services/load-balancers/target-groups.md).
  * Support for [ElastiCache Valkey](../automation-platform/overview/aws-services/database/elastic-cache.md#creating-a-redis-or-valkey-elasticache-instance).
  * Set Retry and Expiration Limits for Asynchronous [Lambda](../automation-platform/overview/aws-services/lambda/) Invocations.
  * Configure [SQS dead letter queues and redrive policies in AWS](../automation-platform/overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/instance-refresh-for-asg.md).
  * Support for Modifying [ASG Launch Templates](../automation-platform/overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/launch-templates.md).
  * [Instance Refresh action for AWS Auto Scaling Groups (ASG)](../automation-platform/overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/instance-refresh-for-asg.md).
  * Customize CloudWatch metrics for [AWS Auto Scaling Groups (ASG)](../automation-platform/overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/#creating-autoscaling-groups-asg).
  * Support for [SNS with FIFO (First-In-First-Out) topics.](../automation-platform/overview/aws-services/sns-topic.md#creating-a-sns-topic)
  * Create scheduled snapshot windows for automated backups in [AWS Redis](../automation-platform/overview-2/azure-services/databases/redis-database.md).
  * Support for [taints with EKS Hosts or Agent Pools](../overview/use-cases/hosts-vms/display-tainted-ec2-hosts.md).
  * [Download inventory reports of all AWS resources](../extras-overview/inventory.md#downloading-an-inventory-report) (for StateRAMP compliance).
  * Support for [Lambda JAR with S3](../automation-platform/overview/aws-services/lambda/#id-3-toc-title).
  * Support for aurora-iopt1 storage type in [Aurora RDS](../aws-user-guide/aws-services/database/rds-database/#id-0-toc-title).
  * Force delete and update settings options added for [ECR repositories](../automation-platform/overview/aws-services/elastic-container-registry-ecr/#updating-ecr-repository-settings).&#x20;
  * Select and update [Certificate Authorities for RDS instances](../aws-user-guide/aws-services/database/rds-database/#managing-rds-certificate-authorities).
  * Specify an initial database during [RDS instance creation](../aws-user-guide/aws-services/database/rds-database/#id-0-toc-title).
  * Support for [serverless Kafka clusters](../automation-platform/overview/aws-services/kafka-cluster.md#creating-a-kafka-cluster) for AWS users.
  * [Disable AWS JIT access for non-admin users](../automation-platform/overview/use-cases/jit-access.md#disabling-jit-access-for-non-admin-users).
  * Support for configuring [S3 bucket replication rules](https://app.gitbook.com/o/ojpRPRrP7bqrzOUuLmOz/s/68cb0s9ce5UIUKWPuYs8/~/changes/1184/overview/aws-services/s3-bucket/~/overview#s3-bucket-replication-rules).
  * Update [RDS Performance Insights](../aws-user-guide/aws-services/database/rds-database/#updating-performance-insights-for-an-existing-rds).
  * Update [ECR repository settings](../automation-platform/overview/aws-services/elastic-container-registry-ecr/).&#x20;
  * [Enable delete protection for AWS Load Balancers.](../automation-platform/overview/aws-services/load-balancers/#additional-load-balancer-settings)
  * Support for adding TLS Hosts and TLS Secrets fields when configuring an[ Ingress for EKS](../kubernetes-overview/ingress-loadbalancer/adding-ingress.md).
  * Automatically redirect incoming HTTP requests to HTTPS for [EKS Ingress](../kubernetes-overview/ingress-loadbalancer/adding-ingress.md).&#x20;
  * Support for [ECS with EC2 Capacity Provider](../automation-platform/overview/aws-services/containers/ecs-containers-and-task-definitions/#configuring-ecs-with-ec2-capacity-provider).
* Azure
  * Add new secret versions in [Azure Key Vault](../automation-platform/overview-2/azure-services/key-vault.md).
  * Support for [Azure Databricks](../automation-platform/overview-2/azure-services/databricks.md).
  * Support for [Azure Container Registry](../automation-platform/overview-2/azure-services/azure-container-registry-acr.md).
  * Support for [Azure Availability Sets](../automation-platform/overview-2/use-cases/hosts-vms/availability-sets.md).
  * Support for [Azure Data Factory](../automation-platform/overview-2/azure-services/data-factory.md).&#x20;
  * [Enable autoscaling in the AKS default node pool](../automation-platform/overview-2/use-cases/infrastructure-and-plan/aks-initial-setup.md).
  * Automatically redirect incoming HTTP requests to HTTPS for [AKS Ingress](../automation-platform/kubernetes-overview/ingress-loadbalancer/aks-ingress/).
* GCP
  * Enable automation to [retain backups when a Cloud SQL instance is deleted](../automation-platform/overview-1/gcp-services/gcp-databases/cloud-sql.md#retaining-backups-before-cloud-sql-deletion).
  * Support for [GCP Virtual Private Cloud (VPC) Peering](../automation-platform/overview-1/gcp-services/virtual-private-cloud-vpc-peering.md).
  * Support for [SNS Pub/Sub topic subscriptions](../automation-platform/overview-1/gcp-services/s3-bucket-3.md#create-a-pub-sub-topic-subscription).
* Kubernetes
  * Support for Running Jobs and CronJobs on [Shared Hosts in AWS](../automation-platform/overview/use-cases/hosts-vms/adding-shared-hosts.md#creating-a-job-or-cronjob-to-run-on-a-shared-host) and [Shared VMs in Azure](../automation-platform/overview/use-cases/hosts-vms/adding-shared-hosts.md#creating-a-job-or-cronjob-to-run-on-a-shared-host).
  * [Manage read-only access to Kubernetes Secrets and ConfigMaps.](../automation-platform/kubernetes-overview/configs-and-secrets/managing-secret-access-for-read-only-users-aws-and-gcp.md)
  * Add custom Kubernetes labels to nodes in AWS at the [host](../automation-platform/overview/use-cases/hosts-vms/) or [Auto Scaling Group](../automation-platform/overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/) (ASG) level.
  * Support for [initContainers and additionalContainers (Sidecar Containers)](../automation-platform/kubernetes-overview/initcontainers-and-sidecar-containers.md) with K8s Services.
* General
  * [Support for granular access control with new Permission Sets.](../automation-platform/security-and-compliance/access-control-2/permission-sets.md)
  * Support for [rolling back container images](../automation-platform/overview/aws-services/containers/container-rollback.md) for DuploCloud Services.
  * [Manage automatic VPN access for new Okta users. ](../automation-platform/access-control/add-and-delete-vpn-access-for-users.md#managing-vpn-access-for-okta-users)
  * Force sync [Okta](../automation-platform/access-control/sso-configuration/okta-identity-management.md) changes to immediately apply updates.
  * DuploCloud UI redesign: updates to navigation, breadcrumbs, menus, and general appearance.
  * [Configure session timeout duration for user logins.](../automation-platform/access-control/session-timeout.md#configuring-session-timeout-for-duplocloud-users)

## Q4 2024

* General
  * DuploCloud's [Advanced Observability Suite (AOS)](../automation-platform/diagnostics-overview/advanced-observability-suite/) is available as an add-on service.

## Q3 2024

* Azure
  * [Set max number of Pods](../automation-platform/overview-2/azure-services/agent-pool/) for Azure Agent Pools.
  * Support for [Table, Queue, and Container storage types](../automation-platform/overview-2/azure-services/storage-account.md#create-storage-account) within Azure Storage Accounts.
* GCP
  * Specify OS disk size when [creating a GCE VM](../automation-platform/overview-1/use-cases/hosts-vms.md#gce-vm).
* Kubernetes
  * [Add Helm repositories and install Helm releases](../automation-platform/kubernetes-overview/helm/helm-charts.md) from the DuploCloud UI.

## Q2 2024

* AWS
  * Support for [Amazon OpenSearch Service domain without EBS](../automation-platform/overview/aws-services/elasticsearch.md#creating-an-opensearch-domain-without-ebs-storage) (Elastic Block Store).
  * Configure [admin-only access to the SSH key](../automation-platform/overview/use-cases/hosts-vms/ssh-ec2-instance.md#configuring-admin-only-access-to-the-ssh-key).
  * Support for[ secondary indexes](../automation-platform/overview/aws-services/database/dynamodb.md#adding-dynamodb-database-tables) when using DynamoDB databases.
  * [Set a maximum RDS instance size ](../automation-platform/overview/aws-services/database/rds-database/restrict-rds-instance-size.md)in Systems Settings.
  * [Support for editing in Apache Airflow](../automation-platform/overview/aws-services/managed-airflow.md).
  * Set up [Billing Alerts](../automation-platform/diagnostics-overview/configure-billing-alerts.md).
  * [Specify a Lambda architecture](../automation-platform/overview/aws-services/lambda/#id-3-toc-title) when creating a Lambda function.
  * Support for[ Instance (Worker Nodes) or IP (Pod IPs) target types](../kubernetes-overview/ingress-loadbalancer/adding-ingress.md#adding-ingress-redirect-config-and-annotations) when creating an EKS Ingress.&#x20;
* Azure
  * Support for [Azure VM Disk Controller](../automation-platform/overview-2/use-cases/hosts-vms/).
  * Specify the cluster type, node VM size, and outbound connectivity source when [creating an AKS cluster](../automation-platform/overview-2/use-cases/infrastructure-and-plan/aks-initial-setup.md#enabling-the-aks-kubernetes-cluster).
  * Support for [private DNS zones](../automation-platform/overview-2/prerequisites/program-dns-entries.md).
  * Configure private endpoints for [MSSQL Server databases](../automation-platform/overview-2/azure-services/databases/sql-database.md#creating-the-mssql-server).
  * Support for [Azure agent pools](../automation-platform/overview-2/azure-services/agent-pool/#adding-an-agent-pool) with availability zones.&#x20;
  * Configure [Redis databases](../automation-platform/overview-2/azure-services/databases/redis-database.md#configure-public-network-access-for-databases-optional) with public network access.&#x20;
  * Support for [PostgreSQL Flexible Server](../automation-platform/overview-2/azure-services/databases/postgresql-flexible-server.md) databases.
  * Support for [Azure Application Gateway SSL policies with AKS Ingress](../automation-platform/kubernetes-overview/ingress-loadbalancer/aks-ingress/using-an-azure-application-gateway-ssl-policy-with-ingress.md) for ALB Load Balancers.
  * Support for [private endpoints ](../automation-platform/overview-2/azure-services/storage-account.md#create-a-private-endpoint)with Azure Storage Account.
  * [Specify the AKS version and Network plugin](https://docs.duplocloud.com/docs/overview-2/use-cases/infrastructure-and-plan/aks-initial-setup) when enabling the AKS cluster.&#x20;
  * Specify the [node resource group](../automation-platform/overview-2/use-cases/infrastructure-and-plan/aks-initial-setup.md) when configuring an AKS cluster.
  * [Specify a computer name](../automation-platform/overview-2/use-cases/hosts-vms/#adding-a-host-vm) when creating a Host.&#x20;
* GCP
  * [Configure a friendly image name under Plan.](../automation-platform/overview-1/use-cases/hosts-vms.md#configuring-a-friendly-image-name)
  * Select [single, or multi-region data location types](../automation-platform/overview-1/gcp-services/s3-bucket-2.md#creating-a-gcp-cloud-storage-bucket) for GCP Storage buckets.&#x20;
  * Configure the [minimum number of ports per VM instance](../automation-platform/overview-1/use-cases/hosts-vms.md#increasing-minimum-ports-per-vm-instance-gke-standard).
* Kubernetes
  * Integrate DuploCloud-managed K8s clusters with [FluxCD](../extras-overview/fluxcd.md).
  * Support for [migration from Flux v1 to Flux v2](../extras-overview/fluxcd.md#migrating-from-flux-v1-to-flux-v2) for FluxCD users.&#x20;
  * Configure [read-only access to K8s Secrets](../automation-platform/kubernetes-overview/configs-and-secrets/managing-secret-access-for-read-only-users-aws-and-gcp.md).
  * Create and manually run a [K8s Job](../automation-platform/kubernetes-overview/jobs.md) from a Kubernetes CronJob.
  * Configure faults for failed [Jobs](../automation-platform/kubernetes-overview/jobs.md#jobs-level-kubernetes-jobs-faults) and [CronJobs ](../kubernetes/cronjobs.md)at the Tenant level.
  * Support for [DaemonSet](https://docs.duplocloud.com/docs/kubernetes-overview/daemonset#creating-a-daemonset-in-duplocloud-aws-or-gcp) with GCP or AWS.&#x20;
* General
  * Enhanced access to [DuploCloud help options](welcome-to-duplocloud/duplocloud-support-model.md#how-to-get-help-from-within-the-duplocloud-portal) from the DuploCloud Platform.&#x20;
  * [Skip faults for stopped Tenant instances.](../automation-platform/diagnostics-overview/faults-and-alarms/#muting-faults-for-stopped-tenants)
  * [Configure user access to multiple Tenants](../automation-platform/access-control/tenant-access/) with one step.
  * [Configure Okta](../automation-platform/access-control/sso-configuration/okta-identity-management.md) as a user source for the DuploCloud Portal.
  * [Customize the text on the login button](../automation-platform/access-control/login-banner-customization.md#adding-custom-login-banner-button-text) for custom banners.

## Q1 2024

* AWS
  * Configure [Automatic Failover for Redis](../automation-platform/overview/aws-services/database/elastic-cache.md#creating-a-redis-elasticache-instance).
  * [Synch AWS Redis with Amazon CloudWatch Logs](../automation-platform/overview/aws-services/database/elastic-cache.md#creating-a-redis-elasticache-instance) for automatic log delivery.
  * Configure [AWS JIT session timeout](../automation-platform/overview/use-cases/jit-access.md#configuring-admin-jit-timeout-via-aws-iam-role) using an IAM role.
  * [Enable automatic AWS ACM (SSL) Certificates](../automation-platform/overview/prerequisites/acm-certificate.md#enabling-automatic-aws-acm-certificate-creation) for a Plan.
  * [Configure K8s Ingress redirect ](../kubernetes-overview/ingress-loadbalancer/adding-ingress.md#configure-ingress-with-redirect-config-and-annotations)using a container port name.
  * [Disable faults for Target Groups without instances.](../automation-platform/overview/use-cases/faults-and-alarms/system-settings-flags.md#disabling-faults-for-target-groups-without-instances)
  * [Enable UltraWarm Data nodes ](../automation-platform/overview/aws-services/elasticsearch.md)for OpenSearch domains.
  * Support for [upgrading EKS components](../automation-platform/overview/use-cases/creating-an-infrastructure-and-plan-for-aws/upgrading-eks-version.md#updating-eks-components-add-ons) (add-ons).&#x20;
  * [Add a Web App Firewall URL](../automation-platform/overview/aws-services/web-application-firewall-waf.md#creating-a-web-application-firewall-waf) when creating or updating a Plan.
  * [Update or skip a final RDS snapshot](../automation-platform/overview/aws-services/database/rds-database/backup-and-restore.md#updating-or-skipping-final-snapshot).
  * [Upgrade the EKS Cluster](../automation-platform/overview/use-cases/creating-an-infrastructure-and-plan-for-aws/upgrading-eks-version.md).
  * Create an [OpenSearch](../automation-platform/overview/aws-services/elasticsearch.md) domain. &#x20;
  * [Billing option is available per Tenant](../automation-platform/overview/use-cases/cost-management/#view-billing-details-by-tenant).
  * [Scale to or from zero (0) using Auto-Scaling Groups](../automation-platform/overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/scale-to-or-from-zero.md).&#x20;
  * Create [Lambdas with Ephemeral Storage](../automation-platform/overview/aws-services/lambda/#id-3-toc-title).
  * Support for [Lambda Dead Letter Queues](../automation-platform/overview/aws-services/lambda/#id-3-toc-title).
  * [Set a delivery delay for SQS Queues](../automation-platform/overview/aws-services/sqs-queue.md#creating-a-standard-queue), using increments of seconds.
  * Configure [Vanta compliance controls](../automation-platform/overview/security-configuration-settings/vanta-compliance-controls.md) for DuploCloud Tenants.
  * Support for [OpenSearch storage options](../automation-platform/overview/aws-services/elasticsearch.md).
  * [Security Configurations Settings](../automation-platform/overview/security-configuration-settings/) documentation section added.
  * Cluster IP and Worker Node target types are supported when creating [EKS Ingress](../kubernetes-overview/ingress-loadbalancer/adding-ingress.md).
* GCP
  * Additional supported actions for [Cloud SQL databases](../automation-platform/overview-1/gcp-services/s3-bucket-1.md#create-a-cloud-scheduler-job) (GCP Console, Edit, Delete, Stop, Restart, or Reset Password)
  * [GKE Standard mode](/broken/pages/30DoAjkzaRTATeeq673S) is supported when creating DuploCloud Infrastructures.
  * Support for [Firestore ](../automation-platform/overview-1/gcp-services/gcp-databases/firestore-database.md)databases.
  * Support for [GCP Hosts](../automation-platform/overview-1/use-cases/hosts-vms.md#id-3-toc-title) and [GCE VMs](../automation-platform/overview-1/use-cases/hosts-vms.md#gce-vm).
  * Create [Node Pools](../automation-platform/overview-1/gcp-services/node-pools.md) with support for accelerators and taints.
  * Support for [GKE Ingress.](../automation-platform/kubernetes-overview/ingress-loadbalancer/gke-ingress.md)
* CI/CD
  * [Update a service with a stream-lined, read-to-use GitHub Actions script](../introduction-to-ci-cd/github-actions/update-a-service.md).
* Kubernetes
  * [Enable real-time alerts for autoscaling Kubernetes nodes.](../automation-platform/overview/use-cases/hosts-vms/auto-scaling/kubernetes-scaling-options.md#allowing-real-time-alerts-for-autoscaling-kubernetes-nodes)
* General&#x20;
  * Restrict open access to public Load Balancers for [AWS](../automation-platform/overview/aws-services/load-balancers/#restricting-open-access-to-public-load-balancers),[ Azure](../automation-platform/overview-2/azure-services/load-balancers.md#restricting-open-access-to-public-load-balancers), and [GCP](../automation-platform/overview-1/gcp-services/step-4-create-a-load-balancer.md#restricting-open-access-to-public-load-balancers).&#x20;
  * Support for [NIST-800-171 compliance](../automation-platform/security-and-compliance/access-control-4.md).
  * [Customize the DuploCloud login screen banner.](../automation-platform/access-control/login-banner-customization.md)
  * [Set Tenants to expire](../automation-platform/overview/use-cases/tenant-environment/tenant-expiry.md) at specified dates and times.
  * Configure settings for all new Tenants under a Plan using [Tenant Config tab](../automation-platform/overview/use-cases/tenant-environment/tenant-config-settings.md).
  * SIEM - [Configure agents to install on specific Tenants.](../automation-platform/security-and-compliance/access-control-3/agent-management.md#agent-setup)

## Q4 2023

* AWS
  * Enable [Spot Instances](../automation-platform/overview/use-cases/hosts-vms/auto-scaling/auto-scaling-groups/spot-instances.md) for EKS Autoscaling Groups (ASG).
  * Implement [Kubernetes Lifecycle Hooks](../automation-platform/kubernetes-overview/kubernetes-lifecycle-hooks.md) while Adding a DuploCloud EKS/Native Service.&#x20;
  * Enable [shared hosts](../automation-platform/overview/use-cases/hosts-vms/adding-shared-hosts.md) to allow K8s Pods in a Tenant to run on Hosts in another Tenant.&#x20;
  * Set a [default automated backup retention period](../automation-platform/overview/aws-services/database/rds-database/backup-and-restore.md#id-0-toc-title-1) for RDS databases.
  * Enable bucket versioning when [creating an S3 bucket](../automation-platform/overview/aws-services/s3-bucket.md#creating-an-s3-bucket).&#x20;
  * Create an [Amazon Machine Image (AMI)](../automation-platform/overview/use-cases/hosts-vms/create-amazon-machine-image-ami.md).
  * Use [dedicated hosts](../automation-platform/overview/use-cases/hosts-vms/adding-dedicated-hosts.md) to launch Amazon EC2 instances and provide additional visibility and control over how instances are placed on a physical server.
  * [Automatically reboot a host](../automation-platform/overview/use-cases/hosts-vms/configure-auto-reboot.md) upon Status Check faults or Host disconnection.
  * Support for [SNS Topic Alerts](../automation-platform/overview/use-cases/faults-and-alarms/sns-topic-alerts.md), enabling notifications and alerts across different AWS services and external endpoints.
  * [Establish VPN connections for private endpoints](../automation-platform/overview/use-cases/creating-an-infrastructure-and-plan-for-aws/kubernetes-cluster/enable-eks-endpoints.md#enabling-vpn-for-private-visibility-optional) when creating an Infrastructure.
  * Restore an [RDS to a particular point in time](../automation-platform/overview/aws-services/database/rds-database/backup-and-restore.md#restoring-snapshots-to-a-point-in-time).
  * Dynamically [change the configuration of a Kafka Cluster](../automation-platform/overview/aws-services/kafka-cluster.md#changing-the-configuration-of-a-kafka-cluster).
  * Fields for Sort Key and Key Type are now available when [creating a DynamoDB](../automation-platform/overview/aws-services/database/dynamodb.md).
* Azure
  * Create a [MySQL Flexible Serve](../automation-platform/overview-2/azure-services/databases/mysql-flexible-server.md)r managed database service.
  * Add an [Azure Service Bus](../automation-platform/overview-2/azure-services/service-bus.md).
* Kubernetes
  * [Follow logs](../automation-platform/overview/aws-services/containers/eks-containers-and-services/#kubernetes-containers) for K8s containers in real-time.&#x20;
  * Influence Pod scheduling by specifying K8s YAML for [Pod Toleration](../automation-platform/kubernetes-overview/pod-toleration.md).&#x20;
  * Create [Kubernetes Jobs (K8s Jobs)](../automation-platform/kubernetes-overview/jobs.md) in AWS and GCP  to manage short-lived, batch workloads in a Kubernetes cluster.
  * Create [Kubernetes CronJobs](../kubernetes/cronjobs.md) in AWS and GCP to schedule long-term K8s Jobs to run at preset intervals.
*   General updates

    * The DuploCloud UI contains numerous design, navigation, and usability improvements, including new menus for managing an RDS, Containers, and Hosts. These improvements are cross-platform and apply to AWS, Azure, and GCP.
    * Quickly search the DuploCloud Portal for any navigation menus or tab labels, such as **Kubernetes Secrets** and **Spend by Month**, using the **Search** box at the top center of the DuploCloud Portal.<br>

    <div align="left"><figure><img src="../.gitbook/assets/search_menu.png" alt=""><figcaption><p>The <strong>Search</strong> box in the DuploCloud Portal<br></p></figcaption></figure></div>

    * Refer to the [Supported Third-Party Tools](../automation-platform/automation-and-tools/supported-third-party-tools.md) page for a list of out-of-the-box functionalities DuploCloud supports.
    * DuploCloud no longer supports launch configurations. Instead, launch templates are created. If you use launch configurations, DuploCloud automatically converts them to launch templates with no interruption in uptime.&#x20;

## August 2023 and September 2023

* AWS
  * [Hibernate an EC2](../automation-platform/overview/use-cases/hosts-vms/hibernate-an-ec2-host.md) host instance.
  * Display [Taints in ECS hosts on unreachable Nodes](../overview/use-cases/hosts-vms/display-tainted-ec2-hosts.md).

## June 2023 and July 2023

* AWS
  * Manage [Tenant expiration and Tenant session durations](../automation-platform/overview/use-cases/tenant-environment/tenant-session-duration.md).
  * Set a [monitoring interval for an RDS](../automation-platform/overview/aws-services/database/rds-database/add-monitoring-interval.md) database.
  * [Enable or disable logging for an RDS ](../automation-platform/overview/aws-services/database/rds-database/enable-or-disable-rds-logging.md)database.
  * Add [custom Lambda image configurations](../automation-platform/overview/aws-services/lambda/create-lambda-using-container-image.md) and URLs.
  * Enable [Object Lock in S3 Buckets](../automation-platform/overview/aws-services/s3-bucket.md#creating-an-s3-bucket) to prevent objects from being deleted or overwritten.&#x20;
  * Configure a [custom S3 Bucket for auditing](../automation-platform/overview/use-cases/creating-an-infrastructure-and-plan-for-aws/ecs-setup/enable-ecs-logging.md#configuring-a-custom-s3-bucket-for-auditing-in-another-aws-account).
  * Update [Lifecycle Policies for EFS storage](../automation-platform/overview/aws-services/elastic-file-system-efs/#updating-efs-lifecycle-policies).
  * [Customize a Node Selector for EKS Services](../automation-platform/overview/aws-services/containers/#adding-a-customized-node-selector-to-an-eks-service) to prevent overrides of specific configurations.
  * Access [ECS container task shells](../automation-platform/overview/prerequisites/kubectl-shell.md#view-the-ecs-task-shell) directly from the DuploCloud Portal.
  * Ability to designate [Essential Containers](../automation-platform/overview/aws-services/containers/#7-toc-title-2) in Task definitions for ECS Services.
  * [Automate fault healing](../automation-platform/overview/use-cases/faults-and-alarms/automatic-fault-healing.md) on EC2 Hosts that fail a status check.
  * Enhanced support for [Startup Probes](../automation-platform/kubernetes-overview/setting-up-probes.md).
* GCP
  * Support for [Redis database instances](../automation-platform/overview-1/gcp-services/gcp-databases/managed-redis.md).
  * Support for [SQL databases](../automation-platform/overview-1/gcp-services/gcp-databases/cloud-sql.md).
  * Change [Cloud Armour Security Policies](../automation-platform/overview-1/gcp-services/cloud-armour.md#modifying-a-cloud-armour-configuration-security-policy).
* General updates
  * **Last Login** card available for determining the last user sign-in when [viewing user access](../automation-platform/access-control/add-edit-or-delete-a-user.md#view-users).
  * [Grant access to specific databases](../automation-platform/access-control/database-access-for-users.md) to non-administrators.

## May 2023

* AWS
  * [Enable EKS endpoints](../automation-platform/overview/use-cases/creating-an-infrastructure-and-plan-for-aws/kubernetes-cluster/enable-eks-endpoints.md) in a DuploCloud Infrastructure, in a more cost-effective and secure manner. Enabling endpoints in DuploCloud allows your network communication to remain internal to the network, without using NAT gateways.&#x20;
  * [Multiple containers](../automation-platform/overview/aws-services/containers/#7-toc-title) are now supported in the ECS **Task Definitions** tab.
  * [Start, stop, and restart ](../automation-platform/overview/aws-services/containers/#7-toc-title-3)up to twenty (20) services at one time.
  * [Add VPC Endpoints](../automation-platform/overview/use-cases/creating-an-infrastructure-and-plan-for-aws/add-vpc-endpoints.md) to a DuploCloud Infrastructure to create a private connection to supported AWS services and VPC endpoint services powered by AWS PrivateLink.
  * [Enable logging for ECS containers](../automation-platform/overview/use-cases/creating-an-infrastructure-and-plan-for-aws/ecs-setup/enable-ecs-logging.md).
  * Define [S3 bucket policies](../automation-platform/overview/aws-services/s3-bucket.md#setting-s3-bucket-permissions-and-policies).
  * Support for [Lambda Layers](../automation-platform/overview/aws-services/lambda/lambda-layers.md) has been added.
  * [CloudWatch EventBridge](/broken/pages/S87qQdzGqKAcEj8m6Kku) rules and targets are supported.
  * The CloudFront feature and associated UI tab have been relocated in the DuploCloud Portal from the **Cloud Services -> App Integration** menu item to the **Cloud Services -> Networking** menu item.
* Azure
  * Support for [Redis databases](../automation-platform/overview-2/azure-services/databases/redis-database.md) is available.
* GCP
  * [Cloud Armour](../automation-platform/overview-1/gcp-services/cloud-armour.md) is supported, to monitor your cloud infrastructures and deployed applications against cyber-attacks.

## April 2023

* AWS
  * Define [custom CIDRs](../automation-platform/overview/aws-services/load-balancers/#adding-a-network-load-balancer-nlb-listener-with-a-custom-cidr) for NLB Load Balancers.
  * Manage multiple Load Balancer settings using the **Load Balancer** tab's [**Other Settings** card](../automation-platform/overview/aws-services/load-balancers/#additional-load-balancer-settings). Settings include specifying a Web Application Firewall (WAF) Access Control List (ACL), enabling HTTP to HTTPS redirects, enabling Access Logs, setting an Idle Timeout, and an option to drop invalid headers.
  * Specify [custom public and private EKS endpoints](../automation-platform/overview/use-cases/creating-an-infrastructure-and-plan-for-aws/kubernetes-cluster/enable-eks-endpoints.md) for your DuploCloud Infrastructure during or after creating an Infrastructure.&#x20;
  * Gain [Cross-Tenant access to restricted policy-based resources](../automation-platform/access-control/tenant-access/cross-tenant-access.md#cross-tenant-access-to-restricted-policy-based-resources).
  * [JIT Access to the AWS Console is redesigned](../automation-platform/overview/use-cases/jit-access.md#obtaining-aws-access-for-a-workstation) with several usability enhancements.
  * [Enable Control Plane logging for EKS clusters](../automation-platform/overview/use-cases/creating-an-infrastructure-and-plan-for-aws/kubernetes-cluster/enable-eks-logs.md).
  * Enable [Read-only processing for ECS services](../automation-platform/overview/aws-services/containers/#enabling-read-only-processing-for-ecs-services).
  * Support for [Aurora RDS Serverless and MySQL read replicas](../automation-platform/overview/aws-services/database/rds-database/add-an-rds-read-replica/add-aurora-rds-replicas.md) and ability to modify Serverless replica instance size.
  * Improved documentation for [upgrading an EKS cluster version](../automation-platform/overview/use-cases/creating-an-infrastructure-and-plan-for-aws/upgrading-eks-version.md).
* Azure
  * [Add a direct link to the Azure Console ](../automation-platform/overview-2/use-cases/azure-portal-link.md)from the DuploCloud **Host** page.
* General Updates
  * [Set read-only access to specific Tenants](../automation-platform/access-control/tenant-access/read-only-access-to-a-tenant.md) for DuploCloud users.

## March 2023

* AWS
  * [Virtual Private Cloud (VPC) peering](../automation-platform/overview/aws-services/virtual-private-cloud-vpc-peering.md) is supported to facilitate data transfer between VPCs.
  * [EMR Serverless](../automation-platform/overview/aws-services/emr-serverless.md) is supported to run open-source big data analytics frameworks without configuring, managing, and scaling clusters or servers.
  * DuploCloud users can obtain [Just-In-Time (JIT) access](../automation-platform/overview/use-cases/jit-access.md) to the AWS Console.
  * [AWS SQS Standard and FIFO queues](../automation-platform/overview/aws-services/sqs-queue.md) are now supported.
  * Use the DuploCloud Portal to work with AWS [Internet of Things (IoT)](../automation-platform/overview/aws-services/iot-internet-of-things.md).
  * Support for Redis database versions when [creating Elastic Cache (Ecache)](../automation-platform/overview/aws-services/database/elastic-cache.md).
  * Enable [shell access for ECS, Kubernetes, and Native docke](../automation-platform/overview/prerequisites/kubectl-shell.md)r containers using a simplified workflow.
  * Reduce storage cost and increase performance by [setting GP3 as your default storage class](../automation-platform/overview/aws-services/storage/gp3-storage-class.md).
  * Enable [NAT Gateways for High Availability (HA)](../automation-platform/overview/aws-services/nat-gateway-for-ha.md).
  * [Restart up to twenty DuploCloud Services](../automation-platform/overview/aws-services/containers/#7-toc-title-1) at once.
* GCP
  * Updated documentation for supported databases.
* CI/CD
  * Documentation for [Bitbucket Pipelines](../automation-platform/introduction-to-ci-cd/bitbucket-pipelines/) is available, which allows developers to automatically build, test, and deploy their code every time they push changes to an Atlassian Bitbucket repository.&#x20;
* Terraform&#x20;
  * Added `IdleTimeout` to [`duplocloud_aws_load_balancer` resource](https://registry.terraform.io/providers/duplocloud/duplocloud/latest/docs/resources/aws_load_balancer).&#x20;

## February 2023

* AWS
  * Enable Elastic Kubernetes Service (EKS) for your existing infrastructure. EKS versions 1.22 and 1.23 are supported.
  * [Timestream databases](../automation-platform/overview/aws-services/database/timestream-database.md) are now supported.
* General updates
  * [Delete VPN connections](../automation-platform/access-control/add-and-delete-vpn-access-for-users.md) for users.

## December 2022 and January 2023

* AWS
  * [AWS ElastiCache](../automation-platform/overview/aws-services/database/elastic-cache.md), a managed caching service for Redis and Memcached, is now supported.&#x20;
  * Monitor Tenant usage in [Cost Management for billing](../automation-platform/overview/use-cases/cost-management/) with weekly or monthly views. After clicking the **Spend by Tenant** tab, select the **shared** card to display tax and support costs.
  * Maintain cluster stability with [Ingress Health Checks annotations](../kubernetes-overview/ingress-loadbalancer/adding-ingress.md#add-load-balancer-with-kubernetes-nodeport).&#x20;
  * Use the [K8s Admin dashboard to monitor StatefulSets](../automation-platform/overview/use-cases/monitoring/kubernetes-administrator-dashboard.md).
  * [Force creation of StatefulSets](../automation-platform/overview/aws-services/containers/#5-toc-title).
* Azure
  * Support for [Kubernetes Ingress](../automation-platform/kubernetes-overview/ingress-loadbalancer/aks-ingress/).
  * Monitor Tenant usage in the [Cost Management for billing ](../automation-platform/overview-2/use-cases/billing-and-cost-management/cost-management.md)feature with weekly or monthly views.
  * Edit [Azure agent pools](../automation-platform/overview-2/azure-services/agent-pool/#editing-an-agent-pool), used to run Azure Kubernetes (AKS) workloads.
* GCP
  * Monitor Tenant usage in the [Cost Management for billing](../automation-platform/overview-1/use-cases/cost-management/) feature with weekly or monthly views.&#x20;
* Kubernetes (K8s)
  * Support for [Kubernetes Ingress in Azure](../automation-platform/kubernetes-overview/ingress-loadbalancer/aks-ingress/).
  * Maintain cluster stability with [Ingress Health Checks annotations](../kubernetes-overview/ingress-loadbalancer/adding-ingress.md#add-load-balancer-with-kubernetes-nodeport) for AWS.&#x20;
  * [Force creation of StatefulSets in AWS](../automation-platform/overview/aws-services/containers/#5-toc-title).
  * Use the K8s Admin dashboard to [monitor StatefulSets in AWS](../automation-platform/overview/use-cases/monitoring/kubernetes-administrator-dashboard.md).
  * Edit [Azure agent pools](../automation-platform/overview-2/azure-services/agent-pool/#editing-an-agent-pool), used to run Azure Kubernetes (AKS) workloads.

## November 2022

* [Ability to add Path-Based Routing rules](../automation-platform/overview/aws-services/load-balancers/#2d32): Configure path-based routing rules for application load balancers.
* [Support for Aurora Serverless V2](../aws-user-guide/aws-services/database/rds-database/#create-aurora-serverless-v2-cluster-database): User can create and manage Aurora Serverless V2 RDS.
* [Billing License Usage](../automation-platform/overview/use-cases/cost-management/duplocloud-license-usage.md): Overview of DuploCloud License Usage according to current service usage.

## October 2022

* [Ability to add Logging Infra at Tenant Level](../automation-platform/overview/use-cases/central-logging/central-logging-setup.md#adding-logging-setup-at-tenant-level): Support to configure logging setup other than default tenant.
* [Support multiple docker registry credentials in a single tenant](../automation-platform/overview/aws-services/containers/#add-multiple-docker-registry-credentials): The user can configure multiple docker registry credentials from the plan.

## September 2022

* [Support for Amazon Managed Apache Airflow](../automation-platform/overview/aws-services/managed-airflow.md): Ability to configure AWS Managed Airflow
* [Configure custom prefix for S3](../automation-platform/overview/aws-services/s3-bucket.md#add-custom-prefix-for-s3-buckets):  Ability to configure a prefix for S3 bucket names.
* [Azure Support to add Storage account](../automation-platform/overview-2/azure-services/storage-account.md): Create Storage Accounts, File Shares, and generate Shared Access Signature (SAS).&#x20;
* Multiple [Azure User Enhancements](../automation-platform/overview-2/azure-services/) were made.

## August 2022

* [Support for Elastic File System (EFS)](../automation-platform/overview/aws-services/elastic-file-system-efs/):  Support for adding EFS has been added to DuploCloud. You can create and mount a shared filesystem for an Infrastructure in the DuploCloud Portal.
* [Support for adding Kubernetes Storage Class:](../automation-platform/overview/aws-services/storage/adding-k8s-storage-class.md) Support for Kubernetes Storage Class and Persistent Volumes is now available.
* [Support for Kubernetes Secret Provider Class](../automation-platform/kubernetes-overview/configs-and-secrets/adding-secretproviderclass-custom-resource.md): This provides the ability to integrate AWS parameters and secrets to be available as Kubernetes secrets.
* [Ability to add Lambda using Container Images](../automation-platform/overview/aws-services/lambda/create-lambda-using-container-image.md): Users can now configure an AWS Lambda using Container images.
* [Support to configure RDS Automatic Backup Retention](../automation-platform/overview/aws-services/database/rds-database/backup-and-restore.md#0-toc-title-1):  Administrators can configure RDS Automatic Backup Retention in days at the system level
* [Export Terraform from an existing Tenant](https://github.com/duplocloud/tenant-terraform-generator): Ability to export DuploCloud terraform provider code for an existing DuploCloud Tenant

## July 2022

* [Ability to Automatically generate Alert](https://docs.duplocloud.com/docs/aws/use-cases/alerting-and-notifications/automatic-alert-creation):  Users can now configure automated alarm creation in AWS, to ensure new resources are included in monitoring.
* [Ability to set resource allocation quotas by an Admin](https://docs.duplocloud.com/docs/aws/use-cases/resource-quotas): Administrators would often like to restrict the type of resources that should or should not be provisioned in their environments. This feature allows them to configure those rules via a DuploCloud Plan.
* [Support for Kubernetes Ingress Controller](https://docs.duplocloud.com/docs/aws/aws-services/containers): Support for the K8s Ingress controller has been added, this is a key piece of functionality for traffic routing to a K8s cluster.
* [RDS Snapshot Management](https://docs.duplocloud.com/docs/aws/aws-services/rds-database/manage-rds-snapshots):  Support for RDS database snapshots was added to the DuploCloud Portal, accessible through the RDS page.
* [Terraform Provider updates](https://registry.terraform.io/providers/duplocloud/duplocloud/latest/docs): Expanded support for more resources in the DuploCloud terraform provider, specifically for Microsoft Azure.&#x20;
