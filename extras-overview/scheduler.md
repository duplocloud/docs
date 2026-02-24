---
description: Configure scheduled shutdowns for Tenant resources using the Scheduler.
---

# Scheduler

DuploCloud allows you to automatically shut down Tenant resources, such as EC2 instances and RDS databases, based on defined schedules. This feature is useful for managing costs and conserving resources in development, test, or other non-production environments.

To schedule shutdowns for instances in a Tenant, complete these three steps:

* **Define Periods**: Define specific time ranges and days of the week when shutdowns should occur.
* **Create Schedules**: Group one or more periods and apply them to a particular resource type (EC2 or RDS). Schedules can be either **Group** schedules, which apply to all instances of the selected resource type in a Tenant, or **Individual** schedules, which apply only to the selected instance(s).
* **Assign Schedules**: Assign the schedules to all instances of a resource type in the Tenant  or to specific individual instances.

## Prerequisites

Before you can configure instance schedules, you must first enable the feature in **System Settings**.

1. Navigate to **Administrator** -> **System Settings.**
2. Select the **System Config** tab.
3.  Click **Add**. The **Add Config** pane displays.<br>

    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (647).png" alt="" width="444"><figcaption><p><strong>Add Config</strong> pane </p></figcaption></figure></div>
4. In the **Config Type** list box, select **Flag**.&#x20;
5. In the **Key** field, select **Enable Instance Scheduler**.
6. In the **Value** list box, select **True**.
7. Click **Save**. The **Scheduler** tab will display when viewing any Tenant under **Administrator** -> **Tenants**.

## Creating Shutdown Periods

A **Period** defines the time window and days of the week when a shutdown should occur. Once created or edited, periods can be reused across multiple schedules.

DuploCloud provides several predefined periods, including **office-hours**, **working-days**, and **weekends**, to help you get started quickly. You must edit them to set the appropriate days and start/end times for your environment.

You can also create your own custom periods if the defaults don't match your needs.

To add or edit a period:

1. Navigate to **Administrator** -> **Tenants**.
2. Select the name of the Tenant from the **NAME** column.
3. Select the **Scheduler** tab.
4.  In the **Periods** section, click **Add**. The **Add Period** pane displays.<br>

    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (650).png" alt="" width="438"><figcaption><p><strong>Add Period</strong> pane</p></figcaption></figure></div>
5. Complete the following fields:

<table data-header-hidden><thead><tr><th width="196.22222900390625"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for the period (e.g., <code>weeknights-7pm</code>).</td></tr><tr><td><strong>Begin Time</strong></td><td>Enter the start time in HH:MM format (e.g., <code>19:00</code>). </td></tr><tr><td><strong>End Time</strong></td><td>Enter the end time in HH:MM format (e.g., <code>07:00</code>). </td></tr><tr><td><strong>Weekdays</strong></td><td>Select the days of the week when the shutdown should occur. </td></tr><tr><td><strong>Description</strong></td><td>Optionally, enter a description for this period for internal reference.</td></tr></tbody></table>

6. Click **Save**.&#x20;

## Creating a Schedule

Schedules define how and when shutdown periods are applied to a specific resource type within a Tenant. you can create two types of schedule:

* **Group schedules** are applied to all EC2 or RDS instances of the selected type in the Tenant.
* **Individual schedules** are applied only to the specific instances you select.

{% hint style="info" %}
Each Tenant can have one Group and one Individual schedule per resource type (EC2 or RDS).
{% endhint %}

To create a schedule, follow these steps:

1. Navigate to **Administrator** -> **Tenants**.
2. Select the name of the Tenant from the **NAME** column.
3. Select the **Scheduler** tab.
4.  In the **Schedule** section, click **Add**. The **Add Schedule** pane displays.<br>

    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (653).png" alt="" width="448"><figcaption><p><strong>Add Schedule</strong> pane</p></figcaption></figure></div>
5. Complete the fields as shown in the following table.

<table data-header-hidden><thead><tr><th width="183.77777099609375"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for the schedule (e.g., <code>dev-ec2-weeknights</code>). </td></tr><tr><td><strong>Resource Type</strong></td><td>Select <strong>EC2</strong> or <strong>RDS</strong>. This determines which type of instances the schedule applies to. Schedules are scoped to a single resource type. You must create separate schedules for EC2 and RDS instances.</td></tr><tr><td><strong>Scheduler Type</strong></td><td>Choose how the schedule should be applied:<br>• <strong>Group</strong>: Applies the schedule to <strong>all instances</strong> of the selected resource type within the Tenant.<br>• <strong>Individual</strong>: Applies the schedule to <strong>only the specific instances</strong> you choose later during assignment.</td></tr><tr><td><strong>Periods</strong></td><td>Select one or more previously defined periods. These determine the time ranges and days the schedule will be active.</td></tr><tr><td><strong>Timezone</strong></td><td>Select the time zone the schedule should use.</td></tr><tr><td><strong>Description</strong></td><td>Optionally, enter a description for this schedule.</td></tr></tbody></table>

6. Click **Save**. It may take a few minutes before the created schedule appears as a selectable option when assigning schedules to instances.

{% hint style="info" %}
**Schedule Behavior Summary**

* **Group** schedules apply to _all EC2 or RDS instances_ in the Tenant and do **not** require selecting instances during assignment.
* **Individual** schedules apply only to the _specific instances_ you select during assignment.
* If a resource has **both** a Tenant and an Individual schedule assigned, the **Individual schedule takes precedence**.
{% endhint %}

### Assigning a Schedule to Instances

After creating one or more schedules, the final step is to assign them to resources in the Tenant.

You can choose to:

* Assign a schedule you’ve already created (Group or Individual), or
* Select **None** to ensure that no schedule is applied to the selected instances. This is useful when you want certain instances to remain running at all times, even if a Tenant-level (Group) schedule is in effect.

To assign a schedule, follow these steps:

1. Navigate to **Administrator** -> **Tenants**.
2. Select the name of the Tenant from the **NAME** column.
3. Select the **Scheduler** tab.
4.  In the **Schedule Assignment** section, click **Add**. The **Assign Schedule** pane displays.<br>

    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (654).png" alt="" width="443"><figcaption><p><strong>Assign Schedule</strong> pane</p></figcaption></figure></div>
5. Complete the following fields.

<table data-header-hidden><thead><tr><th width="208.6666259765625"></th><th></th></tr></thead><tbody><tr><td><strong>Instance Type</strong></td><td>Select the resource type (<strong>EC2</strong> or <strong>RDS</strong>). This filters which schedules and instances are shown.</td></tr><tr><td><strong>Assign Schedule</strong></td><td>Choose one of the created schedules. Only schedules that match the selected resource type will appear.<br><br>You can also select <strong>None</strong> to explicitly <strong>remove any assigned schedule</strong> from the selected instance(s). This is useful if you want an instance to <strong>always remain running</strong>, even if a Tenant-wide schedule exists.</td></tr><tr><td><strong>Instances</strong></td><td>- For <strong>Individual</strong> schedules: Select the instances you want to apply the schedule to.<br>- For <strong>Group</strong> schedules: The instance list will be disabled and the schedule will apply to <strong>all instances</strong> of the selected type automatically.<br><br><strong>Note</strong>: If a resource has both a Tenant and an Individual schedule assigned, the Individual schedule takes precedence.</td></tr></tbody></table>

6. Click **Save**. The scheduler runs on AWS’s standard schedule interval, which checks for updates every 5 minutes, therefore it may take up to 5 minutes for the schedule to take effect.<br>
