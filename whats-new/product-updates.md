---
description: New features and enhancements in DuploCloud
coverY: 0
---

# Product updates

## Q4 2023

* AWS
  * DuploCloud no longer supports launch configurations. Instead, launch templates are created. If you use launch configurations, DuploCloud automatically converts them to launch templates with no interruption in uptime.&#x20;
  * Create an [Amazon Machine Image (AMI)](../aws/use-cases/hosts-vms/create-amazon-machine-image-ami.md).
  * Use [dedicated hosts](../aws/use-cases/hosts-vms/adding-dedicated-hosts.md) to launch Amazon EC2 instances and provide additional visibility and control over how instances are placed on a physical server.
  * [Automatically reboot a host](../aws/use-cases/hosts-vms/configure-auto-reboot.md) upon StatusCheck faults or Host disconnection.
  * Support for [SNS Topic Alerts](../aws/use-cases/faults-and-alarms/sns-topic-alerts.md), enabling notifications and alerts across different AWS services and external endpoints.
  * [Establish VPN connections for private endpoints](../aws/use-cases/disaster-recovery/kubernetes-cluster/enable-eks-endpoints.md#enabling-vpn-for-private-visibility-optional) when creating an Infrastructure.
  * Restore an [RDS to a particular point in time](../aws/aws-services/database/rds-database/backup-and-restore.md#restoring-snapshots-to-a-point-in-time).
  * Dynamically [change the configuration of a Kafka Cluster](../aws/aws-services/kafka-cluster.md#changing-the-configuration-of-a-kafka-cluster).
  * Fields for Sort Key and Key Type are now available when [creating a DynamoDB](../aws/aws-services/database/dynamodb.md).
* Azure
  * Create a [MySQL Flexible Serve](../azure/azure-services/databases/mysql-flexible-server.md)r managed database service.
  * Add an [Azure Service Bus](../azure/azure-services/service-bus.md).
* General updates
  * The DuploCloud UI contains numerous design, navigational, and usability improvements, including new menus for managing an [RDS ](../aws/aws-services/database/rds-database/)and [Hosts](../aws/use-cases/hosts-vms.md).

## August 2023 and September 2023

* AWS
  * [Hibernate an EC2](../aws/use-cases/hosts-vms/hibernate-an-ec2-host.md) host instance.
  * Display [Taints in ECS hosts on unreachable Nodes](../aws/use-cases/hosts-vms/display-tainted-ec2-hosts.md).

## June 2023 and July 2023

* AWS
  * Manage [Tenant expiration and Tenant session durations](../aws/use-cases/tenant-environment/set-tenant-session-duration.md).
  * Set a [monitoring interval for an RDS](../aws/aws-services/database/rds-database/add-monitoring-interval.md) database.
  * [Enable or disable logging for an RDS ](../aws/aws-services/database/rds-database/enable-or-disable-rds-logging.md)database.
  * Add [custom Lambda image configurations](../aws/aws-services/lambda/create-lambda-using-container-image.md) and URLs.
  * Enable [Object Lock in S3 Buckets](../aws/aws-services/s3-bucket.md#creating-an-s3-bucket) to prevent objects from being deleted or overwritten.&#x20;
  * Configure a [custom S3 Bucket for auditing](../aws/use-cases/disaster-recovery/ecs-setup/enable-ecs-logging.md#configuring-a-custom-s3-bucket-for-auditing-in-another-aws-account).
  * Update [Lifecycle Policies for EFS storage](../aws/aws-services/elastic-file-system-efs.md#updating-efs-lifecycle-policies).
  * [Customize a Node Selector for EKS Services](../aws/aws-services/containers/#adding-a-customized-node-selector-to-an-eks-service) to prevent overrides of specific configurations.
  * Access [ECS container task shells](../aws/prerequisites/kubectl-shell.md#view-the-ecs-task-shell) directly from the DuploCloud Portal.
  * Ability to designate [Essential Containers](../aws/aws-services/containers/#7-toc-title-2) in Task definitions for ECS Services.
  * [Automate fault healing](../aws/use-cases/faults-and-alarms/automatic-fault-healing.md) on EC2 Hosts that fail a status check.
  * Enhanced support for [Startup Probes](../aws/aws-services/setting-up-probes.md).
* GCP
  * Support for [Redis database instances](../gcp/gcp-services/databases/redis-database-instance.md).
  * Support for [SQL databases](../gcp/gcp-services/databases/sql-databases.md).
  * Change [Cloud Armour Security Policies](../gcp/gcp-services/cloud-armour.md#modifying-a-cloud-armour-configuration-security-policy).
* General updates
  * **Last Login** card available for determining the last user sign-in when [viewing user access](../user-administration/access-control/add-edit-or-delete-a-user.md#view-users).
  * [Grant access to specific databases](../user-administration/access-control/database-access-for-users.md) to non-administrators.

## May 2023

* AWS
  * [Enable EKS endpoints](../aws/use-cases/disaster-recovery/kubernetes-cluster/enable-eks-endpoints.md) in a DuploCloud Infrastructure, in a more cost-effective and secure manner. Enabling endpoints in DuploCloud allows your network communication to remain internal to the network, without using NAT gateways.&#x20;
  * [Multiple containers](../aws/aws-services/containers/#7-toc-title) are now supported in the ECS **Task Definitions** tab.
  * [Start, stop, and restart ](../aws/aws-services/containers/#7-toc-title-3)up to twenty (20) services at one time.
  * [Add VPC Endpoints](../aws/use-cases/disaster-recovery/add-vpc-endpoints.md) to a DuploCloud Infrastructure to create a private connection to supported AWS services and VPC endpoint services powered by AWS PrivateLink.
  * [Enable logging for ECS containers](../aws/use-cases/disaster-recovery/ecs-setup/enable-ecs-logging.md).
  * Define [S3 bucket policies](../aws/aws-services/s3-bucket.md#setting-s3-bucket-permissions-and-policies).
  * Support for [Lambda Layers](../aws/aws-services/lambda/lambda-layers.md) has been added.
  * [CloudWatch EventBridge](../aws/aws-services/cloud-watch.md) rules and targets are supported.
  * The CloudFront feature and associated UI tab have been relocated in the DuploCloud Portal from the **DevOps -> App Integration** menu item to the **DevOps -> Networking** menu item.
* Azure
  * Support for [Redis databases](../azure/azure-services/databases/redis-database.md) is available.
* GCP
  * [Cloud Armour](../gcp/gcp-services/cloud-armour.md) is supported, to monitor your cloud infrastructures and deployed applications against cyber-attacks.

## April 2023

* AWS
  * Define [custom CIDRs](../aws/aws-services/load-balancers/#adding-a-network-load-balancer-nlb-listener-with-a-custom-cidr) for NLB Load Balancers.
  * Manage multiple Load Balancer settings using the **Load Balancer** tab's [**Other Settings** card](../aws/aws-services/load-balancers/#additional-load-balancer-settings). Settings include specifying a Web Application Firewall (WAF) Access Control List (ACL), enabling HTTP to HTTPS redirects, enabling Access Logs, setting an Idle Timeout, and an option to drop invalid headers.
  * Specify [custom public and private EKS endpoints](../aws/use-cases/disaster-recovery/kubernetes-cluster/enable-eks-endpoints.md) for your DuploCloud Infrastructure during or after creating an Infrastructure.&#x20;
  * Gain [Cross-Tenant access to restricted policy-based resources](../user-administration/access-control/tenant-access/cross-tenant-access.md#cross-tenant-access-to-restricted-policy-based-resources).
  * [JIT Access to the AWS Console is redesigned](../aws/use-cases/jit-access.md#obtaining-aws-access-for-a-workstation) with several usability enhancements.
  * [Enable Control Plane logging for EKS clusters](../aws/use-cases/disaster-recovery/kubernetes-cluster/enable-eks-logs.md).
  * Enable [Read-only processing for ECS services](../aws/aws-services/containers/#enabling-read-only-processing-for-ecs-services).
  * Support for [Aurora RDS Serverless and MySQL read replicas](../aws/aws-services/database/rds-database/add-an-rds-read-replica/add-aurora-rds-replicas.md) and ability to modify Serverless replica instance size.
  * Improved documentation for [upgrading an EKS cluster version](../aws/use-cases/disaster-recovery/kubernetes-cluster/upgrading-eks-version.md).
* Azure
  * [Add a direct link to the Azure Console ](../azure/use-cases/azure-portal-link.md)from a DuploCloud **Host** page **Actions** Menu.
* General Updates
  * [Set read-only access to specific Tenants](../user-administration/access-control/tenant-access/read-only-access-to-a-tenant.md) for DuploCloud users.

## March 2023

* AWS
  * [Virtual Private Cloud (VPC) peering](../aws/aws-services/virtual-private-cloud-vpc-peering.md) is supported to facilitate data transfer between VPCs.
  * [EMR Serverless](../aws/aws-services/emr-serverless.md) is supported to run open-source big data analytics frameworks without configuring, managing, and scaling clusters or servers.
  * DuploCloud users can obtain [Just-In-Time (JIT) access](../aws/use-cases/jit-access.md) to the AWS Console.
  * [AWS SQS Standard and FIFO queues](../aws/aws-services/sqs-queue.md) are now supported.
  * Use the DuploCloud Portal to work with AWS [Internet of Things (IoT)](../aws/aws-services/iot-internet-of-things.md).
  * Support for [Redis database versions](../aws/aws-services/database/elastic-cache.md) when creating Elastic Cache (Ecache).
  * Enable [shell access for ECS, Kubernetes, and Native docke](../aws/prerequisites/kubectl-shell.md)r containers using a simplified workflow.
  * Reduce storage cost and increase performance by [setting GP3 as your default storage class](../aws/aws-services/storage/gp3-storage-class.md).
  * Enable [NAT Gateways for High Availability (HA)](../aws/aws-services/nat-gateway-for-ha.md).
  * [Restart up to twenty DuploCloud Services](../aws/aws-services/containers/#7-toc-title-1) at once.
* GCP
  * Updated documentation for [supported databases](../gcp/gcp-services/databases/).
* CI/CD
  * Documentation for [Bitbucket Pipelines](../ci-cd/bitbucket-pipelines/) is available, which allows developers to automatically build, test, and deploy their code every time they push changes to an Atlassian Bitbucket repository.&#x20;
* Terraform&#x20;
  * Added `IdleTimeout` to [`duplocloud_aws_load_balancer` resource](https://registry.terraform.io/providers/duplocloud/duplocloud/latest/docs/resources/aws\_load\_balancer).&#x20;

## February 2023

* AWS
  * Enable Elastic Kubernetes Service (EKS) for your existing infrastructure. EKS versions 1.22 and 1.23 are supported.
  * [Timestream databases](../aws/aws-services/database/timestream-database.md) are now supported.
* General updates
  * [Delete VPN connections](../user-administration/access-control/add-and-delete-vpn-access-for-users.md) for users.

## December 2022 and January 2023

* AWS
  * AWS ElastiCache, a managed caching service for Redis and Memcached, is now supported.&#x20;
  * Monitor Tenant usage in [Cost Management for billing](../aws/use-cases/cost-management/) with weekly or monthly views. After clicking the **Spend by Tenant** tab, you can also select the **shared** card to display tax and support costs.
  * Maintain cluster stability with [Ingress Health Checks annotations](../aws/aws-services/adding-ingress.md#add-load-balancer-with-kubernetes-nodeport).&#x20;
  * Use the [K8s Admin dashboard to monitor StatefulSets](../aws/use-cases/monitoring/kubernetes-administrator-dashboard.md).
  * [Force creation of StatefulSets](../aws/aws-services/containers/#5-toc-title).
* Azure
  * Support for [Kubernetes Ingress](broken-reference).
  * Monitor Tenant usage in the [Cost Management for billing ](../azure/use-cases/cost-management.md)feature with weekly or monthly views.
  * Edit [Azure agent pools](../azure/azure-services/agent-pool.md#editing-an-agent-pool), used to run Azure Kubernetes (AKS) workloads.
* GCP
  * Monitor Tenant usage in the [Cost Management for billing](../gcp/use-cases/cost-management.md) feature with weekly or monthly views.&#x20;
* Kubernetes (K8s)
  * Support for Kubernetes Ingress in [Azure](broken-reference).
  * Maintain cluster stability with [Ingress Health Checks annotations](../aws/aws-services/adding-ingress.md#add-load-balancer-with-kubernetes-nodeport) for AWS.&#x20;
  * [Force creation of StatefulSets in AWS](../aws/aws-services/containers/#5-toc-title).
  * Use the K8s Admin dashboard to [monitor StatefulSets in AWS](../aws/use-cases/monitoring/kubernetes-administrator-dashboard.md).
  * Edit [Azure agent pools](../azure/azure-services/agent-pool.md#editing-an-agent-pool), used to run Azure Kubernetes (AKS) workloads.

## November 2022

* [Ability to add Path-Based Routing rules](../aws/aws-services/load-balancers/#2d32): Configure path-based routing rules for application load balancers.
* [Support for Aurora Serverless V2](../aws/aws-services/database/rds-database/#create-aurora-serverless-v2-cluster-database): User can create and manage Aurora Serverless V2 RDS.
* [Billing License Usage](../aws/use-cases/cost-management/duplocloud-license-usage.md): Overview of DuploCloud License Usage according to current service usage.

## October 2022

* [Ability to add Logging Infra at Tenant Level](../aws/use-cases/central-logging/central-logging-setup.md#adding-logging-setup-at-tenant-level): Support to configure logging setup other than default tenant.
* [Support multiple docker registry credentials in a single tenant](../aws/aws-services/containers/#add-multiple-docker-registry-credentials): The user can configure multiple docker registry credentials from the plan.

## September 2022

* [Support for Amazon Managed Apache Airflow](../aws/aws-services/managed-airflow.md): Ability to configure AWS Managed Airflow
* [Configure custom prefix for S3](../aws/aws-services/s3-bucket.md#add-custom-prefix-for-s3-buckets):  Ability to configure a prefix for S3 bucket names.
* [Azure Support to add Storage account](../azure/azure-services/storage-account.md): Create Storage Accounts, File Shares, and generate Shared Access Signature (SAS).&#x20;
* Multiple [Azure User Enhancements](../azure/azure-services/) were made.

## August 2022

* [Support for Elastic File System (EFS)](../aws/aws-services/elastic-file-system-efs.md):  Support for adding EFS has been added to DuploCloud. You can create and mount a shared filesystem for an Infrastructure in the DuploCloud Portal.
* [Support for adding Kubernetes Storage Class:](../aws/aws-services/storage/adding-k8s-storage-class.md) Support for Kubernetes Storage Class and Persistent Volumes is now available.
* [Support for Kubernetes Secret Provider Class](../aws/aws-services/adding-secretproviderclass-custom-resource.md): This provides the ability to integrate AWS parameters and secrets to be available as Kubernetes secrets.
* [Ability to add Lambda using Container Images](../aws/aws-services/lambda/create-lambda-using-container-image.md): Users can now configure an AWS Lambda using Container images.
* [Support to configure RDS Automatic Backup Retention](../aws/aws-services/database/rds-database/backup-and-restore.md#0-toc-title-1):  Administrators can configure RDS Automatic Backup Retention in days at the system level
* [Export Terraform from an existing Tenant](https://github.com/duplocloud/tenant-terraform-generator): Ability to export DuploCloud terraform provider code for an existing DuploCloud Tenant\


## July 2022

* [Ability to Automatically generate Alert](https://docs.duplocloud.com/docs/aws/use-cases/alerting-and-notifications/automatic-alert-creation):  Users can now configure automated alarm creation in AWS, to make sure any new resource added to their environment is not missed from monitoring.
* [Ability to set resource allocation quotas by an Admin](https://docs.duplocloud.com/docs/aws/use-cases/resource-quotas): Administrators would often like to restrict the type of resources that should or should not be provisioned in their environments. This feature allows them a way to configure those rules via a DuploCloud Plan.
* [Support for Kubernetes Ingress Controller](https://docs.duplocloud.com/docs/aws/aws-services/containers): Support for the K8s Ingress controller has been added, this is a key piece of functionality for traffic routing to a K8s cluster.
* [RDS Snapshot Management](https://docs.duplocloud.com/docs/aws/aws-services/rds-database/manage-rds-snapshots):  Support to manage RDS database snapshot was added to the Portal, accessible through the RDS page.
* [Terraform Provider updates](https://registry.terraform.io/providers/duplocloud/duplocloud/latest/docs): Expanded support for more resources in the DuploCloud terraform provider, specifically for Microsoft Azure.&#x20;
