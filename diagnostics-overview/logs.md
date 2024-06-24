---
description: Logging in DuploCloud using OpenSearch and Kibana
---

# Logs

At DuploCloud, we understand the importance of transparency and accountability. That's why all activities within our platform are logged and can be used for auditing. These logs are saved into OpenSearch and can be easily visualized in Kibana, providing you with a clear and detailed record of your operations. The URL for Kibana is readily available under Diagnostics.

OpenSearch and Kibana will be inside the VPC and cannot be accessed from outside. Connect to the VPN and access these URLs.

## Application log retention policy

DuploCloud retains application logs in two stages: comprehensive tracking and auditing. Initially, logs are available in OpenSearch for 60 days, ensuring immediate access for recent activity analysis. For long-term storage, logs are then archived in S3 for 365 days, catering to compliance and historical data review needs. These retention periods can be customized to meet specific requirements, offering flexibility in log management

![](https://duplocloud.com/wp-content/uploads/2021/11/audit-logs.png)
