# SIEM

We use [Wazuh](https://www.wazuh.com) as the SIEM. The primary functions of the SIEM are:

1. Data Repository
2. Event Processing Rules
3. Dashboard
4. Events and Alerting

Ossec agents are deployed at various endpoints (VMs in Cloud) where they collect events data from various logs like syslogs, virus scan results, NIDS alerts, File Integrity events, etc. Data is sent to the  centralized wazuh server deployed in the tenant named "Compliance" where it undergoes a set of rules to produce events and alerts that are stored in an OpenSearch with a Kibana Dashboard. Data is also ingested from cloud provider sources like CloudTrail, AWS Trusted Advisor, Guard duty, Container registry scans, Azure Security Center and so on.



{% hint style="info" %}
SIEM setup is fully orchestrated and an out-of-box experience. Ossec agents are automatically installed in hosts and kept up to date by the platform.&#x20;
{% endhint %}

Typically one centralized SIEM is used for multiple accounts i.e. one DuploCloud implementation implements the SIEM and more DuploCloud environments can ingest data there.\


<figure><img src="../../.gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>

