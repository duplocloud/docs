# Vulnerabilities

We use ossec for vulnerability detection in hosts. The data is ingested into the SIEM and part of the dashboard. DuploCloud operations team typically patches the VMs every quarter. Go under SIEM -> Dashboard -> Vulnerabilities for the vulnerabilities dashboard. For more information on the implementation, refer to the [Wazuh Vulnerability Detection Guide](https://documentation.wazuh.com/3.9/user-manual/capabilities/vulnerability-detection.html).

<figure><img src="../../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>

In AWS the platform also integrates with AWS inspector for vulnerability scanning.

<figure><img src="../../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>
