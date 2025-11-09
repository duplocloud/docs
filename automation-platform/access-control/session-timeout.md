---
description: Set session timeout for DuploCloud users
---

# Session Timeout

Session timeout in DuploCloud determines how long a user session remains active before requiring re-authentication. Administrators can configure this setting to enhance security by ensuring users are logged out after a defined period of inactivity.

## Configuring session timeout for DuploCloud users

1. In the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Select the **System Config** tab.
3. Click **Add**. The **Add Config** pane displays.&#x20;

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot (73).png" alt=""><figcaption><p>The <strong>Add Config</strong> pane</p></figcaption></figure></div>

1. In the **Config Type** list box, select **AppConfig**.
2. In the **Key** list box, select `Authorization token session duration`.
3. In the **Value** field, enter the session timeout duration in minutes.
4. Click **Submit**. Users will be logged out and must reauthenticate after the set amount of time.
