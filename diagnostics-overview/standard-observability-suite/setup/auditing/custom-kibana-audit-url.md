---
description: Configure a custom Kibana URL for viewing audit logs from DuploCloud
---

# Custom Kibana Audit URL

DuploCloud provides a default Kibana URL for viewing audit logs, but in some cases, this default URL may not work due to specific configurations or network settings. If necessary, you can override it by configuring a custom Kibana URL that points to a different Kibana instance within DuploCloud's.

## **Configuring a Custom Kibana Audit URL**

1. Log in to the **DuploCloud Portal**.
2. Navigate to **Administrator -**> **System Settings** -> **System Config**.
3.  Click **Add**. The **Add Config** pane displays.\


    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (358).png" alt=""><figcaption><p>The <strong>Add Config</strong> pane</p></figcaption></figure></div>
4. Configure the settings as shown in the following table:

<table data-header-hidden><thead><tr><th width="127.11114501953125">Field</th><th>Value</th></tr></thead><tbody><tr><td><strong>Config Type</strong></td><td>Select: <strong>AppConfig</strong></td></tr><tr><td><strong>Key</strong></td><td>Select one of the following keys, depending on the desired configuration:<br>    <br><strong>Kibana Base URL</strong>: This URL points to the proxy or direct access Kibana URL. <br><strong>Kibana Audit URL Template</strong>: This URL template links to Kibana’s Audit logs.</td></tr><tr><td><strong>Value</strong></td><td>Enter the custom URL for the selected key (for example, <code>/proxy/kibana</code> or a specific Kibana dashboard URL with filters already applied).</td></tr></tbody></table>

5.  Click **Submit** to save the configuration.\


    <figure><img src="../../../../.gitbook/assets/Screenshot (359).png" alt=""><figcaption><p>The <strong>System Config</strong> page in the DuploCloud Platform</p></figcaption></figure>

After configuring the Kibana URL in DuploCloud, you can access Kibana Audit data directly from the DuploCloud Portal:

* Navigate to **Administrator** -> **Observability** -> **Audit**.
