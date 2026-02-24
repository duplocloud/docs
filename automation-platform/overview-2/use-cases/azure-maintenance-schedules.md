---
description: Manage Azure maintenance schedules from the DuploCloud Portal
---

# Azure Maintenance Schedules

DuploCloud allows you to configure maintenance schedules for Azure hosts to control when automated platform operations can occur, minimizing downtime during critical business hours. You can create or update a maintenance schedule directly from the DuploCloud Portal for each individual host.

## Creating a Maintenance Schedule

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Hosts**.
2. Select the tab matching the type of host you want to configure a maintenance schedule for (**Host** or **VM Scale Set**.
3. Click on the host name in the **NAME** column.
4. Select the **Maintenance Schedule** tab.
5.  If no schedule is currently configured, click **Enable Maintenance Schedule**.\
    The **Create VM Maintenance Schedule** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (524).png" alt="" width="339"><figcaption><p><strong>Create VM Maintenance Schedule</strong> pane</p></figcaption></figure></div>
6. Complete the following fields:

<table data-header-hidden><thead><tr><th width="177.5555419921875"></th><th></th></tr></thead><tbody><tr><td><strong>Start Time</strong></td><td>Specify the date and time when the maintenance window begins, for example, <strong>2025-06-15 01:00 PM</strong>. Choose a time window that aligns with your application’s low-traffic periods to minimize potential impact.</td></tr><tr><td><strong>Time Zone</strong></td><td>Select the time zone used for scheduling.</td></tr><tr><td><strong>Maintenance window</strong> (<strong>Hours</strong>/<strong>Minutes</strong>)</td><td>Specify the number of hours and minutes the window should last (e.g., 1 hour, 30 minutes).</td></tr><tr><td><strong>Repeats</strong></td><td>Define the recurrence pattern by specifying a number and frequency:<br>• <strong>Day</strong>: Repeats every <em>N</em> days.<br>• <strong>Week</strong>: Prompts you to select one or more weekdays.<br>• <strong>Month</strong>: Prompts you to choose specific dates and/or weekday occurrences.</td></tr><tr><td><strong>Repeats on</strong></td><td>If needed (if <strong>Weekly</strong> or <strong>Monthly</strong> repeats are selected), specify the repeat frequency:<br>• For <strong>Weekly</strong>, select one or more days (e.g., <strong>Monday</strong>).<br>• For <strong>Monthly</strong>, choose dates (e.g., <strong>5</strong>, <strong>20</strong>) or weekday occurrences (e.g., <strong>3rd Friday</strong>).</td></tr><tr><td><strong>End Time</strong></td><td>Optionally, specify the date and time when the recurring schedule should stop. For example, <strong>2025-12-15 01:00 PM</strong>.</td></tr></tbody></table>

7. Click **Save** to activate the schedule. The new schedule appears in the **Maintenance Schedule** tab.

<figure><img src="../../../.gitbook/assets/Screenshot (525).png" alt=""><figcaption><p><strong>Maintenance Schedule</strong> tab</p></figcaption></figure>

## Updating a Maintenance Schedule

You can modify an existing maintenance schedule at any time using the host settings.

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Hosts**.
2. Select the tab that matches the type of host you want to update a maintenance schedule for (**Host** or **VM Scale Set**.
3. Click on the host name in the **NAME** column to open the host details page.
4.  Click the **Actions** men&#x75;**,** select **Host Settings**, and then **Update Maintenance Schedule**. The **Update VM Maintenance Schedule** pane displays, pre-filled with the current settings.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (526) (1).png" alt=""><figcaption><p><strong>Actions</strong> menu</p></figcaption></figure></div>
5.  Modify any of the fields listed in the **Update VM Maintenance Schedule** pane (also listed in the table above).<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (527).png" alt="" width="341"><figcaption></figcaption></figure></div>
6. Click **Save** to apply your changes. Changes may take a few minutes to propagate across Azure systems.
