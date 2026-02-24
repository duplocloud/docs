---
description: Configure session timeout for DuploCloud users
---

# Session Timeout

Session timeout in DuploCloud determines how long a user session remains active before requiring re-authentication. Administrators can configure these settings to enhance security by ensuring users are logged out after a defined period of inactivity.

## Configuring Authorization Token Session Duration

Set how long a user session lasts in the DuploCloud Portal before the user must reauthenticate.

1. In the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Select the **System Config** tab.
3. Click **Add**. The **Add Config** pane displays.&#x20;

<div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (73).png" alt=""><figcaption><p><strong>Add Config</strong> pane</p></figcaption></figure></div>

4. In the **Config Type** list box, select **AppConfig**.
5. In the **Key** list box, select **Authorization token session duration**.
6. In the **Value** field, enter the session timeout duration in minutes.
7. Click **Submit**. Users will be logged out and must reauthenticate after the set amount of time.

## Maximum Kubernetes Session Duration

Set the maximum duration of a Kubernetes session (kubectl shell or K8s dashboard) before reauthentication is required.

1. In the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Select the **System Config** tab.
3. Click **Add**. The **Add Config** pane displays.&#x20;

<div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (1090).png" alt="" width="406"><figcaption><p><strong>Add ConAdd Config</strong> pane<strong>fig</strong> pane</p></figcaption></figure></div>

4. In the **Config Type** list box, select **AppConfig**.
5. In the **Key** list box, select **Maximum K8s Session Duration**.
6. In the **Value** field, enter the session timeout duration in minutes.
7. Click **Submit**. Users will be logged out and must reauthenticate after the set amount of time.
