---
description: Configure Tenant settings in the DuploCloud UI for AWS users
---

# AWS Tenant Settings

## Configuring Tenant settings:&#x20;

1. Navigate to **Administrator** -> **Tenants**.
2. In the **NAME** column, select the name of the Tenant you want to configure settings for.&#x20;
3. Select the **Settings** tab, and click **Add**. The **Add Tenant Feature** pane displays.
4. From the **Select Feature** list box, select the setting (see list of settings below).&#x20;
5. Click **Enable**, or enter an appropriate value.&#x20;
6. Click **Add**. The setting is applied to the Infrastructure.&#x20;

## Tenant Settings

| **Enable Encryption at Rest**                                   | Enables encryption of data at rest within the Tenant.                                                   |
| --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| **Delete Protection**                                           | Enables delete protection for the Tenant.                                                               |
| **Default: Block public access to s3**                          | Sets the default to block public access to S3 buckets for the Tenant.                                   |
| **Default: Enforce SSL for s3**                                 | Sets the default to enforce SSL for S3 for the Tenant.                                                  |
| **Default: Enable bucket versioning for new s3 buckets**        | Sets the default to enable bucket versioning for new S3 buckets for the Tenant.                         |
| **Default: Enable encryption at rest for ES**                   | Sets the default to enable encryption at rest for Elasticsearch (ES) for the Tenant.                    |
| **Default: Enable node to node encryption for ES**              | Sets the default to enable node-to-node encryption for Elasticsearch (ES).                              |
| **Default: Enforce SSL for ES**                                 | Sets the default to enforce SSL for Elasticsearch (ES).                                                 |
| **Default: Use latest TLS cipher for ES**                       | Sets the default to use the latest TLS cipher for Elasticsearch (ES) for the Tenant.                    |
| **Automatically rotate KMS keys**                               | Enables automatic rotation of KMS (Key Management Service) keys for the Tenant.                         |
| **AWS Access Token Validity**                                   | Defines the duration of validity for AWS access tokens for the Tenant.                                  |
| **Enable K8S network policy**                                   | Enables Kubernetes network policies for the Tenant.                                                     |
| **Enable option to run K8S pods on any Host**                   | Enables the option to run the Tenant's Kubernetes (K8S) pods on any available Host.                     |
| **Allow hosts to run K8S pods from other tenants**              | Allows the Tenant's Hosts to run Kubernetes (K8S) pods from other Tenants.                              |
| **Restrict public lb create for non-admin**                     | Restricts the ability to create public Load Balancers (LB) to admin users only.                         |
| **Restrict EC2 instance create in public subnet for non-admin** | Restricts the ability to create EC2 instances in public subnets to admin users only.                    |
| **Restrict non-ssl listener create for non-admin**              | Restricts the ability to create non-SSL listeners to admin users only.                                  |
| **Enable Alerting**                                             | Enables alerting for the Tenant.                                                                        |
| **Enable ECS CloudWatch Logging**                               | Enables ECS (Elastic Container Service) CloudWatch logging for the Tenant.                              |
| **Enable ECS ElasticSearch Logging**                            | Enables ECS (Elastic Container Service) Elasticsearch logging for the Tenant.                           |
| **Enable k8s job fault logging by default**                     | Enables Kubernetes job fault logging by default for the Tenant.                                         |
| **Enable AWS IoT**                                              | Enables the integration of IoT devices with AWS services for the Tenant.                                |
| **AWS IoT Topic Prefix**                                        | Allows setting a topic prefix for AWS IoT within the Tenant.                                            |
| **AWS IoT Thing Prefix**                                        | Allows setting a prefix for naming IoT Things within the Tenant.                                        |
| **AWS Role Max Session Duration**                               | Specifies the maximum session duration for AWS roles.                                                   |
| **Enable Auto Reboot EC2 status check**                         | Enables automatic reboot of the Tenant's EC2 instances when they fail a status check.                   |
| **Enable Auto Reboot K8s Nodes if disconnected**                | Enables automatic reboot of the Tenant's Kubernetes (K8s) nodes if they become disconnected.            |
| **Set SNS Topic Alerts**                                        | Enables setting of SNS (Simple Notification Service) topic alerts for the Tenant.                       |
| **Enable Cluster Autoscaler OverProvisioning**                  | Enables Cluster Autoscaler overprovisioning for the Tenant.                                             |
| **Maximum K8s Session Duration**                                | Specifies the maximum duration for Kubernetes sessions.                                                 |
| **Enable Node monitoring**                                      | Enables node monitoring, allowing for the collection and analysis of metrics and logs.                  |
| **Enable K8S Node Monitoring**                                  | Enables Kubernetes (K8s) node monitoring, allowing for the collection and analysis of metrics and logs. |
| **Enable Docker Monitoring**                                    | Enables Docker monitoring for the Tenant.                                                               |
| **Enable K8S Docker Monitoring**                                | Enable K8S Docker Monitoring for the Tenant.                                                            |
| **Enable Docker Container Logging**                             | Enables Docker container logging, allowing logs from running containers to be captured.                 |
| **Enable Kubernetes Pods Logging**                              | Enables Kubernetes pod logging for the Tenant.                                                          |
| **Other**                                                       | Allows entering a custom or unlisted setting.                                                           |

