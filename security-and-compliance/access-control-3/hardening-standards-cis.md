# Hardening Standards (CIS)

DuploCloud platform orchestrates CIS benchmark monitoring using Wazuh and Ossec for virtual machines. Wazuh provides the Security Configuration Assessment (SCA) module which offers the user the best possible experience when performing scans on hardening and configuration policies. To check the SCA report, go to “Security dashboard Security Events” and search for rule.groups: "sca". For more information, refer to the [Wazuh SCA](https://documentation.wazuh.com/3.12/user-manual/capabilities/sec-config-assessment/).

<figure><img src="../../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>

For cloud provider CIS posture we integrate with AWS security Hub. We also enable several other conformation packs like PCI and AWS Foundational Security Best Practices v1.0.0.&#x20;

For Azure and GCP today it needs to be setup and managed manually out of band from their portals using Azure Security Center and GCP Security Command center respectively. We are slated to release the GCP command center integration sometime in Q2 2024 and Azure in Q4 2024.



<figure><img src="../../.gitbook/assets/image (145).png" alt=""><figcaption></figcaption></figure>
