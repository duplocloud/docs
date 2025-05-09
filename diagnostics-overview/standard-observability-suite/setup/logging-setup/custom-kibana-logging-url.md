---
description: Configure a custom Kibana URL for viewing Logging data from DuploCloud
---

# Custom Kibana Logging URL

DuploCloud provides a default Kibana URL for viewing Logging data, but if you want to update filters or customize further, you can override the default with these settings.

## **Configuring a Custom Kibana Logging URL**

1. Log in to the **DuploCloud Portal**.
2. Navigate to **Administrator** -> **System Settings** -> **System Config**.
3.  Click **Add**. The **Add Config** pane displays.\
    \


    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (343).png" alt=""><figcaption><p>The <strong>Add Config</strong> pane</p></figcaption></figure></div>
4. In the **Config Type** list box, select **AppConfig**.
5. In the **Key** list box, choose one of the following keys:
   * **Kibana Base URL**: This URL points to the proxy or direct access Kibana URL.
   * **Kibana Logs URL Template**: This URL template links to Kibana’s Logs.&#x20;
6. In the **Value** field, enter the custom URL for the selected key. For example:
   * **Kibana Base URL**: `/proxy/kibana`
   * **Kibana Logs URL Template**: `https://kibana.example.com/app/discover#/?_a=(query:(language:kuery,query:'log_type:"application"'))&_g=(time:(from:now-1h,to:now))`

{% hint style="info" %}
You can customize the example URLs, replacing placeholders with your own values and modifying the query string to adjust the filters:

* **log\_type**: Filter by log type (e.g., `"application"`, `"system"`).
* **kubernetes.namespace**: Filter by Kubernetes namespace (e.g., `"default"`).
* **log\_level**: Filter by log level (e.g., `"error"`, `"info"`).
* **time range**: Adjust the time range (e.g., `from:now-1h`, `from:now-7d`).
* **Example**:\
  `https://kibana.example.com/app/discover#/?_a=(query:(language:kuery,query:'log_type:"application"'))&_g=(time:(from:now-1h,to:now))`
{% endhint %}

7. Click **Submit** to save the configuration.

<figure><img src="../../../../.gitbook/assets/Screenshot (360) (1).png" alt=""><figcaption><p>The <strong>System Config</strong> page in the DuploCloud Platform</p></figcaption></figure>

After configuring the Kibana URL in DuploCloud, you can access the selected Kibana Logs data directly from the DuploCloud Portal:

* Navigate to **Administrator** -> **Observability** -> **Standard** -> **Logging**.
