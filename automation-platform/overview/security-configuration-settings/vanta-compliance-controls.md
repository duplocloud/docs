---
description: Configure Vanta compliance controls for your DuploCloud Tenants
---

# Vanta Compliance Controls

DuploCloud applies tags on AWS resources following the Vanta [Bulk Tags](https://help.vanta.com/en/articles/11345627-bulk-tags) feature. This allows the Vanta and AWS GuardDuty to monitor your applications and provide real-time alerts and notifications for compliance issues, security events, and vulnerabilities.

## Enabling Vanta Compliance Controls&#x20;

To enable Vanta compliance controls directly from the DuploCloud Portal:

1. Navigate to **Administrator** -> **Systems Settings**.
2. Click the **Compliance Controls** tab.&#x20;
3. Use the **Enable Vanta Controls** toggle switch to enable Vanta Monitor. GuardDuty is enabled by default when this setting is enabled.&#x20;
4. Enter an email in the **GuardDuty Notifications** Email field. GuardDuty notifications will be sent to this email address.&#x20;
5. From the **Select Tenant** list box, select the Tenant for which Vanta controls will be enabled.&#x20;
6. In the **Tenant Settings for&#x20;**_**YOUR\_TENANT\_NAME**_ area, enter the Tenant **Owner** and **Description**, and indicate whether the Tenant is **Production** and/or **Contains User Data**.
7. Click **Save**. Vanta compliance controls are enabled for the specified Tenant.&#x20;

<figure><img src="../../../.gitbook/assets/compliance controls.png" alt=""><figcaption><p>The <strong>Compliance Controls</strong> page configured to <strong>Enable Vanta Controls</strong>. </p></figcaption></figure>
