---
description: Create and connect to an RDS database instance
---

# RDS database

DuploCloud supports the following RDS databases in AWS:

* MySQL
* PostgreSQL
* MariaDB
* Microsoft SQL-Express
* Microsoft SQL-Web
* Microsoft SQL-Standard
* Aurora MySQL
* Aurora MySQL Serverless
* Aurora PostgreSQL
* Aurora PostgreSQL Serverless

{% hint style="warning" %}
Support for the Aurora Serverless V1 database engines has been deprecated. When using Terraform, do not create V1 engines.
{% endhint %}

## Creating an RDS database <a href="#id-0-toc-title" id="id-0-toc-title"></a>

1. In the DuploCloud Portal, navigate to **DevOps** -> **Database**.
2. Click **Add**. The **Create a RDS** page displays.
3. Fill out the form based on your requirements, and **Enable Logging**, if needed.
4. Optionally, in the **Backup Retention Period in Days** field, enter a number of days to retain automated backups between one (**1**) and thirty-five (**35**). If a value is not entered, the Backup Retention Period value configured in Systems Settings will be applied.&#x20;

<figure><img src="../../../../.gitbook/assets/IAM3.png" alt=""><figcaption><p><strong>Create a RDS</strong> window.</p></figcaption></figure>

#### Create Aurora Serverless V2 Cluster database

You can create Aurora Serverless V2 Databases by selecting **Aurora-MySql-Serverless-V2** or **Aurora-PostgreSql-Serverless-V2** from the **RDS Database Engine** list box. Select the RDS Engine Version compatible with Aurora Serverless v2. The **RDS Instance Size** of `db.serverless` applies to both engines.

## Connecting to the database <a href="#id-1-toc-title" id="id-1-toc-title"></a>

Once the database is created, select it and use the **Instances** tab to view the endpoint and credentials. Use the **Endpoints** and credentials to connect to the database from your application running in an EC2 instance. The database is only accessible from inside the EC2 instance in the current Tenant, including the containers running within.

![RDS Instances tab](../../../../.gitbook/assets/RDS5.png)

{% hint style="info" %}
Pass the endpoint, name, and credentials to your application [using environment variables](../../containers/passing-config-and-secrets.md) for maximum security.&#x20;
{% endhint %}
