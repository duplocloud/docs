---
description: A conceptual overview of DuploCloud Services
---

# Services

A Service could be a Kubernetes Deployment, StatefulSet, or DaemonSet. It can also be a Lambda function or an ECS task or service, capturing a microservice. Each Service (except Lambda) is given a Load Balancer to expose itself and is assigned a DNS name.

{% hint style="info" %}
DuploCloud Services should not be confused with Kubernetes or ECS services. By Service, we mean application components that can be either Docker-based or serverless.
{% endhint %}

## DuploCloud Supported Services

**For information on cloud-specific Services supported by DuploCloud, see:**

* [AWS Services](../../overview/aws-services/)
* [Azure Services](../../overview-2/azure-services/)
* [GCP Services](../../overview-1/gcp-services/)

DuploCloud supports a simple, application-specific interface to configure dozens of cloud services, such as S3, SNS, SQS, Kafka, Elasticsearch, Data Pipeline, EMR, SageMaker, Azure Redis, Azure SQL, Google Redis, etc. Almost all commonly used services are supported, and new ones are constantly added. DuploCloud Engineers fulfill most requests for new Services within days, depending on their complexity.

All Services and cloud features are created within a [Tenant](tenant.md). While users specify application-level constructs for provisioning cloud resources, DuploCloud implicitly adds all the underlying DevOps and compliance controls.

Below is an image of some properties of a Service:

<figure><img src="../../.gitbook/assets/Screenshot (246).png" alt=""><figcaption><p>The <strong>Add Service</strong> page in the DuploCloud Platform</p></figcaption></figure>
