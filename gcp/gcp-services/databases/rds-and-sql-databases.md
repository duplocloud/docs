---
description: Adding RDS and SQL Databases in DuploCloud
---

# RDS and SQL databases

DuploCloud supports a number of RDS and SQL databases, including:

* MySQL
* PostgreSQL
* MariaDB
* Microsoft SQL - Express, Standard, and Web
* Aurora, MySQL, and PostgreSQL - Serverless Versions 1 and 2
* Amazon DocumentDB (DocDB)

Use this procedure to set up each database instance.

## Creating an RDS database

1. In the DuploCloud Portal, navigate to **DevOps** --> **Database**.
2. Click the **RDS** tab.
3. Click **Add**. The **Add RDS** page displays for you to **Create a RDS**.&#x20;
4. Provide the **RDS Name**, **Username**, **Password**, **RDS Engine Version,** and **RDS Instance Size**.&#x20;
5. Click **Submit**.

<figure><img src="../../../.gitbook/assets/GCP_Create_RDS.png" alt=""><figcaption><p><strong>Create a RDS</strong> on the <strong>Add RDS</strong> page </p></figcaption></figure>

## Creating a SQL database

Use this procedure to create:

* MySQL databases
* SQL databases with PostGres engines
* SQL databases with SQLServer engines

1. In the DuploCloud Portal, navigate to **DevOps** --> **Database**.
2. Click the **SQL** tab.
3. Click **Add**. The **Add SQL DB** page displays.&#x20;
4. For MySQL databases and SQL databases with PostGres engines, provide the **Name**, **SQL Version**, and **Tier** (Machine Type/CPU). For SQL databases with SQLServer engines, provide the same inputs, in addition to **Root Password** and **Disk Size** in gigabytes (GB).
5. Click **Create**.&#x20;
6. Select your database from the Name column in the **SQL** tab. The **Details** tab displays information about the database you created.

Refer to the graphics below for examples of creating and displaying the supported SQL databases.

<figure><img src="../../../.gitbook/assets/gcp_Sq1.png" alt=""><figcaption><p><strong>Add SQL DB</strong> page for adding a <strong>MYSQL</strong> database</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/gcp_Sq2.png" alt=""><figcaption><p><strong>Details</strong> tab for a created <strong>MySQL</strong> database</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/gcp_Sq3.png" alt=""><figcaption><p><strong>Add SQL DB</strong> page for adding a SQL database with a <strong>POSTGRES</strong> engine</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/gcp_Sq4.png" alt=""><figcaption><p><strong>Details</strong> tab for created SQL database with a <strong>POSTGRES</strong> engine</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/gcp_Sq5.png" alt=""><figcaption><p><strong>Add SQL DB</strong> page for adding a SQL database with a <strong>SQLSERVER</strong> engine</p></figcaption></figure>



<figure><img src="../../../.gitbook/assets/gcpdbr.png" alt=""><figcaption><p><strong>Details</strong> tab for created SQL database with a <strong>SQLSERVER</strong> engine</p></figcaption></figure>

