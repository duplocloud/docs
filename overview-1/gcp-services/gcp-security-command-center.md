---
description: Utilize GCP Security Command Center with DuploCloud
---

# GCP Security Command Center

The GCP Security Command Center (SCC) integration in DuploCloud provides key security insights—threats, vulnerabilities, and compliance benchmarks—in a unified interface. This page explains how to activate and configure GCP SCC with DuploCloud.

## Prerequisites&#x20;

**Activate Security Command Center in GCP**: Before enabling SCC features in DuploCloud, activate the Security Command Center directly in your GCP account. GCP does not support enabling SCC via API.

**Enable Security Command Center Features in DuploCloud**: Once SCC is activated in GCP, enable and configure it in DuploCloud:

1. In the DuploCloud Portal, go to **Administrator** → **System Settings**.
2. Select the **GCP Account Security** tab.
3. In the **Account** list box, choose your GCP account.
4. Click **Enable Security Command Center**.
5. Enable the following services:
   * **Security Health Analytics**
   * **Web Security Scanner**
   * **Event Threat Detection**
   * **Container Threat Detection**
   * **Virtual Machine Threat Detection**
6. Click **Save Settings**. Security Command Center features are enabled for DuploCloud.

{% hint style="info" %}
&#x20;It may take approximately **24-48 hours** for security findings and data to populate in the DuploCloud Portal.
{% endhint %}

## Viewing GCP Security Insights in DuploCloud

After configuring the GCP Security Command Center (SCC), DuploCloud displays SCC findings directly within the platform to help you identify vulnerabilities, monitor compliance, and respond to threats.

### Threats

To view SCC Threat data from the DuploCloud Portal, navigate to **Security** -> **Threats**.

You can filter threats by their status (Active or Inactive) and severity (High, Medium, or Low), helping you focus on the most urgent incidents.

### Vulnerabilities

To view the Vulnerabilities data in the DuploCloud Portal, navigate to **Security** → **Vulnerabilities**. This dashboard serves as your primary tool for tracking and managing vulnerabilities across your environment, with a focus on high-risk vulnerabilities and their associated findings.

The Vulnerabilities Dashboard provides an overview of your environment's security state. This overview helps you quickly gauge the scale and urgency of your security posture, prioritizing the most critical vulnerabilities and findings that need attention.

<figure><img src="../../.gitbook/assets/Screenshot (270) (1).png" alt=""><figcaption><p>The SCC <strong>Vulnerabilities</strong> Dashboard in the DuploCloud Portal</p></figcaption></figure>

The main Vulnerabilities dashboard also allows you to tab between **By Vulnerability** and **All Findings**:

**By Vulnerability**: This tab lets you explore **Details** or **Findings** for each vulnerability.&#x20;

* The **Details** tab provides an overview of the vulnerability, including its description, associated standards, and the total and active findings linked to the vulnerability.&#x20;
* The **Findings** tab gives a more granular view of each specific finding related to the vulnerability, showing the status, severity, category, and the affected resources.

**All Findings:** This tab allows you to select individual findings to view a detailed summary. You can also view the data in a JSON View format for a detailed, structured, machine-readable representation.

<figure><img src="../../.gitbook/assets/Screenshot (268).png" alt=""><figcaption><p>A detailed summary of the <strong>User Managed Service Account Key</strong> finding</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot (269).png" alt=""><figcaption><p>A JSON view of the <strong>User Managed Service Account Key</strong> finding</p></figcaption></figure>

### Standards

To access and view the SCC Standards Dashboard in the DuploCloud Portal, navigate to **Security** -> **Standards**. This dashboard is your central hub for monitoring and maintaining compliance with industry-recognized security frameworks such as NIST, HIPAA, PCI-DSS, and CIS.

The Standards Dashboard is organized with tabs representing the various security standards. By selecting a standard, you can view a list of rules related to that standard. You can filter rules by Status (Active or Inactive) or Severity (Critical, High, Medium, or Low).

<figure><img src="../../.gitbook/assets/Screenshot (262).png" alt=""><figcaption><p>The SCC <strong>Standards</strong> Dashboard in the DuploCloud Platform</p></figcaption></figure>

Click on a specific rule for deeper insights including **Details** and **Findings**:

**Details**: This tab provides additional details, including a description of the rule, the total number of findings related to the rule (including how many are active), and the associated compliance standards.

<figure><img src="../../.gitbook/assets/Screenshot (265).png" alt=""><figcaption><p>The <strong>Details</strong> tab for the <strong>BUCKET_POLICY_ONLY_DISABLED</strong> rule</p></figcaption></figure>

**Findings:** This tab provides a detailed description of each finding associated with the rule, offering a granular view of compliance issues. It includes the finding Status (Active or Resolved), Severity (Critical, High, Medium, or Low), category (e.g., "Flow logs disabled"), the affected resource, timestamps, and more.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot (264).png" alt=""><figcaption><p>The <strong>Findings</strong> tab for the <strong>BUCKET_POLICY_ONLY_DISABLED</strong> rule</p></figcaption></figure>
