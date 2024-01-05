---
description: Logging for AWS in the DuploCloud Platform
---

# Logs

The DuploCloud platform performs centralized logging for Docker-based applications. For the built-in and Kubernetes container orchestration, this is implemented using OpenSearch and Kibana with Filebeat as the log collector.&#x20;

For ECS Fargate, AWS Lambda, and AWS SageMaker Jobs, the platform integrates with CloudWatch, automatically setting up Log Groups and making them viewable from the DuploCloud Portal.

{% hint style="info" %}
No setup is required to enable logging for ECS Fargate, Lambda, or AWS SageMaker Jobs. DuploCloud automatically sets up CloudWatch log groups and provides a menu next to each resource.&#x20;
{% endhint %}





&#x20;
