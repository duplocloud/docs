---
description: Support for AWS Timestream databases
---

# AWS Timestream database

DuploCloud supports the Amazon Timestream database in the DuploCloud Portal. AWS Timestream is a fast, scalable, and serverless time-series database service that makes it easier to store and analyze trillions of events per day at an accelerated speed.&#x20;

Amazon Timestream automatically scales to adjust for capacity and performance, so you don’t have to manage the underlying infrastructure.

## Adding a Timestream database

1. In the DuploCloud Portal, navigate to **DevOps** -> **Database**.
2.  Click the **Timestream** tab.

    <figure><img src="../../../.gitbook/assets/AWS_Timestream.png" alt=""><figcaption><p><strong>Timestream</strong> database page </p></figcaption></figure>
3.  Click **Add**. The **Add Timestream Database** pane displays.

    <figure><img src="../../../.gitbook/assets/AWS_Add_Timestream_DB.png" alt=""><figcaption><p><strong>Add Timestream Database</strong> pane</p></figcaption></figure>
4. Enter the **DatabaseName.**
5. Select an **Encryption Key**, if required.
6. Click **Submit**. The Timestream database name displays on the **Timestream** tab.

## Adding Tables to a Timestream database

1. In the DuploCloud Portal, navigate to **DevOps** -> **Database**.
2. From the **RDS** page, click the **Timestream** tab.
3. Select the database from the **Name** column.
4.  On the **Tables** tab, click **Add**. The **Add Timestream Table** pane displays.

    <figure><img src="../../../.gitbook/assets/AWS_Add_Timestream_Table.png" alt=""><figcaption><p><strong>Add Timestream Table</strong> pane</p></figcaption></figure>
5. Enter the **Table Name** and other necessary information to size and create your table.
6. Click **Create**.

## Modifying and Running a Timestream database

1. In the DuploCloud Portal, navigate to **DevOps** -> **Database**.
2. From the **RDS** page, click the **Timestream** tab.
3. Select the database from the **Name** column.
4. On the Timestream page, click the database's **Action** menu to modify the **JSON** code or launch the **Console** in AWS. You can also select the database name in the **Name** column and, from the **Table** tab, click the table's **Action** menu to modify the **JSON** code or launch the **Console** in AWS or **Delete** a table.

<figure><img src="../../../.gitbook/assets/AWS_Timestream_Action.png" alt=""><figcaption><p><strong>Actions</strong> menu for a <strong>Timestream</strong> database, <strong>Table</strong> tab</p></figcaption></figure>
