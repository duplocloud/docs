---
description: CIS benchmark monitoring using Wazuh and Ossec for Hosts
---

# Hardening Standards (CIS)

The DuploCloud platform orchestrates CIS benchmark monitoring for virtual machines using Wazuh and Ossec. Wazuh provides the Security Configuration Assessment (SCA) module which offers the user the best possible experience when performing scans on hardening and configuration policies. To check the SCA report, navigate to the **SIEM** dashboard and click **Security Events**. Using the search field, enter **rule.groups: "sca"**. For more information, refer to the [Wazuh SCA](https://documentation.wazuh.com/3.12/user-manual/capabilities/sec-config-assessment/).

<figure><img src="../../../.gitbook/assets/image (409).png" alt=""><figcaption><p><strong>SIEM</strong> dashboard <strong>Security Events</strong> tab in the DuploCloud Portal</p></figcaption></figure>

DuploCloud integrates with AWS Security Hub for cloud provider CIS posture and enables several other conformation packs, such as PCI and AWS Foundational Security Best Practices v1.0.0. DuploCloud also integrates with corresponding security services in GCP and Azure.

<figure><img src="../../../.gitbook/assets/image (403).png" alt=""><figcaption><p>The <strong>Secuity</strong> -> <strong>Standards</strong> page in the DuploCloud Portal</p></figcaption></figure>
