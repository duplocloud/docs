---
description: Logging for AWS in the DuploCloud Platform
---

# Logs

The DuploCloud Platform performs centralized logging for [Docker](https://www.docker.com/)-based applications. For the native and [Kubernetes ](https://kubernetes.io/)container orchestrations, this is implemented using [OpenSearch ](https://opensearch.org/docs/latest/install-and-configure/install-opensearch/docker/)and [Kibana ](https://www.elastic.co/kibana)with [Elastic Filebeat](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-overview.html) as the log collector.&#x20;

For ECS Fargate, AWS Lambda, and AWS SageMaker Jobs, the platform integrates with CloudWatch, automatically setting up Log Groups and making them viewable from the DuploCloud Portal.

{% hint style="info" %}
No setup is required to enable logging for ECS Fargate, Lambda, or AWS SageMaker Jobs. DuploCloud automatically sets up CloudWatch log groups and provides a menu next to each resource.&#x20;
{% endhint %}





&#x20;
