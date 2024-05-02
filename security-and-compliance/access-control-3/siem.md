# SIEM

We use [Wazuh](https://wazuh.com/) as the SIEM. The primary functions of the SIEM are:

1. Data Repository
2. Event Processing Rules
3. Dashboard
4. Events and Alerting

Ossec agents are deployed at various endpoints (VMs in the Cloud) where they collect event data from various logs like syslogs, virus scan results, NIDS alerts, File Integrity events, etc. Data is sent to the centralized Wazuh server deployed in the **Compliance** Tenant, where it undergoes a set of rules to produce events and alerts stored in an OpenSearch with a Kibana Dashboard. Data is also ingested from cloud provider sources like CloudTrail, AWS Trusted Advisor, Guard duty, Container registry scans, Azure Security Center, etc.

{% hint style="info" %}
If a customer desires SIEM, setup is fully orchestrated as an an out-of-the-box experience. The platform automatically installs and updates Ossec agents in the DuploCloud Hosts.&#x20;
{% endhint %}

Typically, one centralized SIEM is used for multiple accounts, i.e., one DuploCloud implementation implements the SIEM, and more DuploCloud environments can ingest data there.\


<figure><img src="../../.gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>

