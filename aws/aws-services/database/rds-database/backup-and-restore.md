---
description: >-
  Backing up your resources with snapshots, virtual machine snapshots/VM AMI,
  and automated backup.
---

# Backup and restore

## Creating a snapshot <a href="#0-toc-title" id="0-toc-title"></a>

1. In the DuploCloud Portal, select **DevOps** -> **Database**
2. &#x20;Click the **RDS** tab, and **select your database name**.&#x20;
3. From the **Actions** item list, select **Backup & Restore**
4. Select **Create Snapshot**.&#x20;
5. The **confirmation pane** displays. Click **Confirm**.

<div align="left">

<figure><img src="../../../../.gitbook/assets/Screenshot (149).png" alt=""><figcaption><p>The <strong>Actions</strong> menu on the <strong>DevOps</strong> <strong>Database</strong> page, <strong>RDS</strong> tab.</p></figcaption></figure>

</div>

## Viewing RDS database  <a href="#0-toc-title" id="0-toc-title"></a>

You can view your RDS instance/cluster in JSON or directly on the AWS Console.&#x20;

1. In the DuploCloud Portal, select **DevOps** -> **Database**
2. Click the **RDS** tab, and **select your database name**.&#x20;
3. From the **Actions** item list, select **View**.
4. Select **View JSON** or **Console** to view your RDS database in JSON or directly on the AWS Console.&#x20;

<div align="left">

<figure><img src="../../../../.gitbook/assets/Screenshot (150).png" alt=""><figcaption><p>The <strong>Actions</strong> menu with <strong>View</strong> selected to view an RDS database.</p></figcaption></figure>

</div>

## Enabling Automated Backup Retention period <a href="#0-toc-title" id="0-toc-title"></a>

1. In the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Click the **System Config** tab.
3. Click **Add**. The **Add Config** pane displays.
4. From the **Config Type** list box, select **AppConfig**.
5. From the **Name** list box, select **RDS Automated Backup Retention days**.
6. In the **Value** field, enter the **number of days (1-35)** you would like your backups to be retained.

{% hint style="info" %}
The backup retention period would be applied to the new databases created after configuring the system settings.&#x20;
{% endhint %}

<div align="left">

<img src="../../../../.gitbook/assets/image (63).png" alt="Configure RDS Backup Retention">

</div>

## Restoring a snapshot <a href="#1-toc-title" id="1-toc-title"></a>

Once the backups are done, they will be available to be restored on the next instance creation.

![Create a RDS page](https://duplocloud.com/wp-content/uploads/2021/11/db-restore.png)
