---
description: Manage backup and restore for Relational Database Services (RDS)
---

# Backup and restore

## Creating a snapshot <a href="#id-0-toc-title" id="id-0-toc-title"></a>

Create a [snapshot ](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER\_WorkingWithAutomatedBackups.html)of an RDS.

1. In the DuploCloud Portal, navigate to **DevOps** -> **Database**.
2. In the **RDS** tab, in the row containing your RDS instance, click the **Actions** menu icon ( <img src="../../../../.gitbook/assets/Kabab_three_Vertical_dots (5) (1).png" alt="" data-size="line"> ) and select **Backup & Restore** -> **Create Snapshot**.&#x20;
3. **Confirm** the snapshot request. Once taken, the snapshot displays in the **Snapshot** tab.

<div align="left">

<img src="../../../../.gitbook/assets/RDSpit1 (1).png" alt="RDS Tab with Actions menu for DUPLODEV01-DOCS instance with Create Snapshot option highlighted">

</div>

## Restoring a snapshot <a href="#id-1-toc-title" id="id-1-toc-title"></a>

Once backups are available, you can restore them on the next instance creation when you [create an RDS](./#0-toc-title).

<div align="left">

<img src="../../../../.gitbook/assets/res5 (1).png" alt="Create a RDS page with Create from Snapshot option">

</div>

## Restoring snapshots to a point in time

You can restore available RDS snapshots to a specific point in time.

1. In the DuploCloud Portal, navigate to **DevOps** -> **Database**.
2. In the **RDS** tab, select an RDS instance containing [snapshots](backup-and-restore.md#0-toc-title).
3. Click the **Snapshots** tab.
4. Click the Actions menu and select **Backup & Restore** -> **Restore to Point in Time**. The **Restore Point in Time** pane displays.
5. In the **Target Name** field, append the RDS name to the prefilled _`TENANT_NAME`_ prefix.
6. Select either the **Last Restorable Time** or **Custom date and time** option. If you select the **Custom date and time** option, specify the date and time in the format indicated.
7. Click **Submit**. Your selected RDS is restored to the point in time you specified.&#x20;

## Setting an RDS automated backup retention period <a href="#id-0-toc-title" id="id-0-toc-title"></a>

&#x20;can set backup retention periods in the DuploCloud Portal.

1. In the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Select the **System Config** tab.
3. Click **Add**. The Config pane displays.
4. From the **Config Type** list box, select **AppConfig**.
5. From the **Key** list box, select **RDS Automated Backup Retention days**.
6. In the **Value** field, enter the number of days to retain the backup, from one (**1**) to thirty-five (**35**) days.
7. Click Submit. The System Configs area in the System Config tab is updated with the retention period you entered for the **RDS Automated Backup Retention days** key.

<div align="left">

<img src="../../../../.gitbook/assets/res4.png" alt="Add Config pane with Key RDS Automated Backup Retention days">

</div>

{% hint style="info" %}
The backup retention period  new databases.&#x20;
{% endhint %}
