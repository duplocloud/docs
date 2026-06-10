---
description: AWS services available within your Environments — with links to full documentation.
---

# Services

The following AWS services are available within the AWS Extension. Each service is provisioned and managed inside an [Environment](../policy-model/environment.md). Full documentation for each service is maintained in the AWS User Guide.

## Compute and Containers

| Service | Description |
|---|---|
| [Containers and Services](../../automation-platform/overview/aws-services/containers/README.md) | EKS, ECS, and native Docker workloads |
| [EKS Containers and Services](../../automation-platform/overview/aws-services/containers/eks-containers-and-services/README.md) | Kubernetes-based container workloads on EKS |
| [ECS Containers, Task Definitions and Services](../../overview/aws-services/containers/ecs-containers-and-task-definitions/README.md) | Container workloads on Elastic Container Service |
| [App Runner](../../automation-platform/overview/aws-services/app-runner.md) | Fully managed container application service |
| [Batch](../../automation-platform/overview/aws-services/batch.md) | Managed batch computing workloads |
| [Lambda Functions](../../overview/aws-services/lambda/README.md) | Serverless function execution |
| [EMR Serverless](../../automation-platform/overview/aws-services/emr-serverless.md) | Serverless big data processing with Apache Spark and Hive |

## Networking and Content Delivery

| Service | Description |
|---|---|
| [Load Balancers](../../automation-platform/overview/aws-services/load-balancers/README.md) | Application and network load balancers for EKS, ECS, and Docker services |
| [API Gateway](../../automation-platform/overview/aws-services/api-gateway.md) | Managed HTTP, REST, and WebSocket APIs |
| [CloudFront](../../automation-platform/overview/aws-services/cloudfront/README.md) | Content delivery network (CDN) with distributions, functions, and key-value stores |
| [NAT Gateway for HA](../../automation-platform/overview/aws-services/nat-gateway-for-ha.md) | High-availability NAT gateway configuration |
| [Virtual Private Cloud (VPC) Peering](../../automation-platform/overview/aws-services/virtual-private-cloud-vpc-peering.md) | Direct network connectivity between VPCs |
| [Web App Firewall (WAF)](../../automation-platform/overview/aws-services/web-application-firewall-waf.md) | Web application firewall for filtering malicious traffic |

## Storage

| Service | Description |
|---|---|
| [Storage Classes and PVCs](../../automation-platform/overview/aws-services/storage/README.md) | Kubernetes persistent storage on EBS |
| [S3 Bucket](../../overview/aws-services/s3-bucket.md) | Object storage with bucket notifications |
| [Elastic File System (EFS)](../../automation-platform/overview/aws-services/elastic-file-system-efs/README.md) | Managed shared file storage for EC2 and containers |
| [Elastic Container Registry (ECR)](../../automation-platform/overview/aws-services/elastic-container-registry-ecr/README.md) | Private container image registry |

## Databases

| Service | Description |
|---|---|
| [RDS](../../aws-user-guide/aws-services/database/rds-database/README.md) | Managed relational databases — MySQL, PostgreSQL, MariaDB, SQL Server, Oracle, and Aurora |
| [AWS ElastiCache](../../automation-platform/overview/aws-services/database/elastic-cache.md) | Managed Redis and Memcached in-memory data stores |
| [AWS DynamoDB](../../aws-user-guide/aws-services/database/dynamodb.md) | Fully managed NoSQL key-value and document database |
| [AWS Timestream](../../automation-platform/overview/aws-services/database/timestream-database.md) | Managed time-series database |

## Messaging and Streaming

| Service | Description |
|---|---|
| [SNS Topic](../../automation-platform/overview/aws-services/sns-topic.md) | Managed pub/sub messaging |
| [SQS Queue](../../automation-platform/overview/aws-services/sqs-queue.md) | Managed message queuing |
| [Kinesis Stream](../../automation-platform/overview/aws-services/kinesis-stream.md) | Real-time data streaming |
| [Kafka Cluster](../../automation-platform/overview/aws-services/kafka-cluster.md) | Managed Apache Kafka on Amazon MSK |
| [Amazon MQ](../../automation-platform/overview/aws-services/amazon-mq.md) | Managed message broker for ActiveMQ and RabbitMQ |
| [EventBridge](../../automation-platform/overview/aws-services/eventbridge.md) | Serverless event bus for application integration |

## Data and Analytics

| Service | Description |
|---|---|
| [Managed Airflow](../../automation-platform/overview/aws-services/managed-airflow.md) | Managed Apache Airflow for workflow orchestration |
| [Data Pipeline](../../automation-platform/overview/aws-services/data-pipeline.md) | Managed data pipeline for moving and processing data |

## Security

| Service | Description |
|---|---|
| [AWS Secrets Manager](../../automation-platform/overview/aws-services/aws-secrets-manager.md) | Managed storage and rotation of secrets and credentials |

## IoT

| Service | Description |
|---|---|
| [IoT (Internet of Things)](../../automation-platform/overview/aws-services/iot-internet-of-things.md) | Managed IoT device connectivity and message routing |
