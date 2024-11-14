---
description: Logging in DuploCloud using OpenSearch and Kibana
---

# Logs

In the standard observability suite DuplolCloud has OpenSearch built in. File beat is used as a collector deployed in each host. It is viewable under Admin --> Observability --> Standard --> Logs and under the tenant context Observability --> Standard --> Logs. In the Tenant context ready made filters are available for easy access to logs per service in that tenant. Further filters can be created using Kibana interface. DuploCloud's filebeat collector automatically labels the logs with tenant, service, containers and other such meta data. &#x20;

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

## Application log retention policy

DuploCloud retains application logs in two stages: comprehensive tracking and auditing. Initially, logs are available in OpenSearch for 60 days, ensuring immediate access for recent activity analysis. For long-term storage, logs are then archived in S3 for 365 days, catering to compliance and historical data review needs. These retention periods can be customized to meet specific requirements, offering flexibility in log management
