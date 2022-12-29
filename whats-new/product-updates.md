---
description: New features and enhancements in DuploCloud
---

# Product updates

### December 2022 and January 2023

* GCP
  * Monitor Tenant usage in the [Billing feature](https://app.gitbook.com/o/ojpRPRrP7bqrzOUuLmOz/s/68cb0s9ce5UIUKWPuYs8/\~/changes/LIQrEoD3lxoJfvhsSCPM/gcp/use-cases/cost-management) with weekly or monthly views.&#x20;
* Kubernetes (K8s)
  * [Force creation of StatefulSets](../aws/aws-services/containers/#0-toc-title).
  * Maintain cluster stability with Ingress Health Checks annotations.&#x20;
* AWS
  * Enable [Elastic Kubernetes Service (EKS)](../aws/use-cases/kubernetes-cluster/) for your existing infrastructure. EKS versions 1.22 and 1.23 are supported.
  * AWS ElastiCache, a managed caching service for Redis and Memcached, is now supported.&#x20;
  * Monitor Tenant usage in the [Billing feature](../aws/use-cases/cost-management/) with weekly or monthly views. In the Tenant view's **shared** card, tax and support costs are now displayed.
* Azure
  * Edit [Azure agent pools](../azure/azure-services/agent-pool.md#editing-an-agent-pool), used to run Azure Kubernetes (AKS) workloads.
  * Monitor Tenant usage in the [Billing feature](https://app.gitbook.com/o/ojpRPRrP7bqrzOUuLmOz/s/68cb0s9ce5UIUKWPuYs8/\~/changes/7ev96ixoUE2TKhw2W8yw/azure/use-cases/cost-management) with weekly or monthly views.



### November 2022

* [Ability to add Path-Based Routing rules](../aws/use-cases/load-balancers.md#2d32): Configure path-based routing rules for application load balancers.
* [Support for Aurora Serverless V2](../aws/aws-services/rds-database/#create-aurora-serverless-v2-cluster-database): User can create and manage Aurora Serverless V2 RDS.
* [Billing License Usage](../aws/use-cases/cost-management/duplocloud-license-usage.md): Overview of DuploCloud License Usage according to current service usage.

### October 2022

* [Ability to add Logging Infra at Tenant Level](../aws/use-cases/central-logging/central-logging-setup.md#adding-logging-setup-at-tenant-level): Support to configure logging setup other than default tenant.
* [Support multiple docker registry credentials in a single tenant](../aws/aws-services/containers/#add-multiple-docker-registry-credentials): The user can configure multiple docker registry credentials from the plan.

### September 2022

* [Support for Amazon Managed Apache Airflow](../aws/aws-services/managed-airflow.md): Ability to configure AWS Managed Airflow
* [Configure custom prefix for S3](../aws/aws-services/s3-bucket.md#add-custom-prefix-for-s3-buckets):  Ability to configure a prefix for S3 bucket names.
* [Azure Support to add Storage account](../azure/azure-services/storage-account.md): Create Storage Accounts, File Shares, and generate Shared Access Signature (SAS).&#x20;
* Multiple [Azure User Enhancements](../azure/azure-services/) were made.

### August 2022

* [Support for Elastic File System (EFS)](../aws/aws-services/elastic-file-system-efs.md):  Support for adding EFS has been added to DuploCloud. You can create and mount a shared filesystem for an Infrastructure in the DuploCloud Portal.
* [Support for adding Kubernetes Storage Class:](../aws/aws-services/containers/adding-k8s-storage-class.md) Support for Kubernetes Storage Class and Persistent Volumes is now available.
* [Support for Kubernetes Secret Provider Class](../aws/aws-services/containers/adding-secretproviderclass-custom-resource.md): This provides the ability to integrate AWS parameters and secrets to be available as Kubernetes secrets.
* [Ability to add Lambda using Container Images](../aws/aws-services/lambda/create-lambda-using-container-image.md): Users can now configure an AWS Lambda using Container images.
* [Support to configure RDS Automatic Backup Retention](../aws/aws-services/rds-database/backup-and-restore.md#0-toc-title-1):  Administrators can configure RDS Automatic Backup Retention in days at the system level
* [Export Terraform from an existing Tenant](https://github.com/duplocloud/tenant-terraform-generator): Ability to export DuploCloud terraform provider code for an existing DuploCloud Tenant\


### July 2022

* [Ability to Automatically generate Alert](https://docs.duplocloud.com/docs/aws/use-cases/alerting-and-notifications/automatic-alert-creation):  Users can now configure automated alarm creation in AWS, to make sure any new resource added to their environment is not missed from monitoring.
* [Ability to set resource allocation quotas by an Admin](https://docs.duplocloud.com/docs/aws/use-cases/resource-quotas): Administrators would often like to restrict the type of resources that should or should not be provisioned in their environments. This feature allows them a way to configure those rules via a DuploCloud Plan.
* [Support for Kubernetes Ingress Controller](https://docs.duplocloud.com/docs/aws/aws-services/containers): Support for the K8 Ingress controller has been added, this is a key piece of functionality for traffic routing to a K8 cluster.
* [RDS Snapshot Management](https://docs.duplocloud.com/docs/aws/aws-services/rds-database/manage-rds-snapshots):  Support to manage RDS database snapshot was added to the Portal, accessible through the RDS page.
* [Terraform Provider updates](https://registry.terraform.io/providers/duplocloud/duplocloud/latest/docs): Expanded support for more resources in the DuploCloud terraform provider, specifically for Microsoft Azure.&#x20;
