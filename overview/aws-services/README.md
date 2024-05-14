---
description: Managing AWS services and related components
---

# AWS Services

Applications are written involving many AWS Services like S3 for Object Store, RDS for RDBS (SQL), Redis, Kafka, SQS, SNS, Elastic Search, and so on. While each of their configurations needs a few application-centric inputs, there are scores of lower-level nuances around access control, security, and compliance among others.

Using DuploCloud you can pretty much create any service within the Tenant using basic app-centric inputs while the platform will make sure the lower-level nuances are programmed to best practices for security and compliance.&#x20;

## Exposing Services to multiple Tenants (Cross-tenant Access)

Every service within the Tenant will automatically be reachable to any application running within that tenant. If you need to expose some service from one Tenant to another, see [Allow Cross-tenant Access](../../access-control/tenant-access/cross-tenant-access.md).

{% hint style="info" %}
DuploCloud adds new AWS services to the platform on almost a weekly basis, if a certain service is not documented here please contact the DuploCloud Team. Even if the feature is currently available, the DuploCloud team will enable the feature in a matter of days.
{% endhint %}

## Supported Services for DuploCloud AWS

Supported Services are listed in alphabetical order, following the core services:  Containers, Load Balancers, and Storage.

### Core Services

* [Containers and Services](containers/)
* [Load Balancers](load-balancers/)
* [Storage](../../aws-user-guide/aws-services/storage/)

### Additional Services

* [API Gateway](../../aws-user-guide/aws-services/api-gateway.md)
* [Batch](batch.md)
* [CloudFront](cloudfront.md)
* [Databases](database/)
* [Data Pipeline](data-pipeline.md)
* [Elastic File System (EFS)](elastic-file-system-efs/)
* [EMR Serverless](emr-serverless.md)
* [EventBridge](cloud-watch.md)
* [Ingress (Kubernetes)](../../kubernetes-overview/ingress-loadbalancer/adding-ingress.md)
* [IoT (Internet of Things)](iot-internet-of-things.md)
* [Kafka Cluster](kafka-cluster.md)
* [Kinesis Stream](kinesis-stream.md)
* [Lambda functions](lambda/)
* [Managed Airflow](managed-airflow.md)
* [NAT Gateway for High Availability (HA)](nat-gateway-for-ha.md)
* [OpenSearch](elasticsearch.md)
* [Probes and Health Check](setting-up-probes.md)
* [S3 Bucket](s3-bucket.md)
* [SNS Topic](sns-topic.md)
* [SQS Queue](sqs-queue.md)
* [Virtual Private Cloud (VPC) Peering ](virtual-private-cloud-vpc-peering.md)
* [Web App Firewall (WAF)](web-application-firewall-waf.md)

