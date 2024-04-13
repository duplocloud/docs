# File Integrity Monitoring

The platform leverages ossec to implement FIM. Agents on the hosts will monitor the key files for any changes, verifying the checksum and attributes of the monitored files. The System Check will happen every 12 hours. To check the file integrity monitoring, go to “SIEM Dashboard Integrity Monitoring”. For more information, refer to the [Wazuh Vulnerability Detection Guide](https://documentation.wazuh.com/3.9/user-manual/capabilities/file-integrity/index.html).

<figure><img src="../../.gitbook/assets/image (150).png" alt=""><figcaption></figcaption></figure>
