---
description: Managing AWS services and related components
---

# AWS Services

Applications are written involving many AWS Services like S3 for Object Store, RDS for RDBS (SQL), Redis, Kafka, SQS, SNS, Elastic Search, and so on. While each of their configurations needs a few application-centric inputs, there are scores of lower-level nuances around access control, security, and compliance among others.

Using DuploCloud you can pretty much create any service within the Tenant using basic app-centric inputs while the platform will make sure the lower-level nuances are programmed to best practices for security and compliance.&#x20;

{% hint style="info" %}
DuploCloud adds new AWS services to the platform frequently. If a certain service is not documented here please contact the DuploCloud Team. Often new features can be enabled in a matter of days.&#x20;
{% endhint %}

## Supported Services for DuploCloud AWS

Supported Services are listed in alphabetical order, following the core services: Containers and Load Balancers.

### Core Services

* [Containers and Services](../../automation-platform/overview/aws-services/containers/)
* [Load Balancers](../../automation-platform/overview/aws-services/load-balancers/)

### Additional Services

* [API Gateway](../../automation-platform/overview/aws-services/api-gateway.md)
* [App Runner](../../automation-platform/overview/aws-services/app-runner.md)
* [Batch](../../automation-platform/overview/aws-services/batch.md)
* [CloudFront](../../automation-platform/overview/aws-services/cloudfront/)
* [Databases](../../automation-platform/overview/aws-services/database/)
  * [AWS ElastiCache](../../automation-platform/overview/aws-services/database/elastic-cache.md)
  * [AWS DynamoDB database](../../aws-user-guide/aws-services/database/dynamodb.md)
  * [AWS Timestream database](../../automation-platform/overview/aws-services/database/timestream-database.md)
  * [RDS database](../../aws-user-guide/aws-services/database/rds-database/)
* [Data Pipeline](../../automation-platform/overview/aws-services/data-pipeline.md)
* [Elastic Container Registry (ECR)](../../automation-platform/overview/aws-services/elastic-container-registry-ecr/)
* [Elastic File System (EFS)](../../automation-platform/overview/aws-services/elastic-file-system-efs/)
* [EMR Serverless](../../automation-platform/overview/aws-services/emr-serverless.md)
* [EventBridge](../../automation-platform/overview/aws-services/eventbridge.md)
* [Ingress (Kubernetes)](../../kubernetes-overview/ingress-loadbalancer/adding-ingress.md)
* [IoT (Internet of Things)](../../automation-platform/overview/aws-services/iot-internet-of-things.md)
* [Kafka Cluster](../../automation-platform/overview/aws-services/kafka-cluster.md)
* [Kinesis Stream](../../automation-platform/overview/aws-services/kinesis-stream.md)
* [Lambda functions](lambda/)
* [Managed Airflow](../../automation-platform/overview/aws-services/managed-airflow.md)
* [Amazon MQ](../../automation-platform/overview/aws-services/amazon-mq.md)
* [NAT Gateway for High Availability (HA)](../../automation-platform/overview/aws-services/nat-gateway-for-ha.md)
* [OpenSearch](../../automation-platform/overview/aws-services/elasticsearch.md)
* [S3 Bucket](s3-bucket.md)
* [SNS Topic](../../automation-platform/overview/aws-services/sns-topic.md)
* [SQS Queue](../../automation-platform/overview/aws-services/sqs-queue.md)
* [Virtual Private Cloud (VPC) Peering](../../automation-platform/overview/aws-services/virtual-private-cloud-vpc-peering.md)
* [Web App Firewall (WAF)](../../automation-platform/overview/aws-services/web-application-firewall-waf.md)
