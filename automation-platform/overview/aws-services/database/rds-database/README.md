---
description: Create and connect to an RDS database instance
---

# RDS database

Create, configure, and manage RDS instances directly from the DuploCloud Portal.

DuploCloud supports the following RDS databases in AWS:

| <p></p><ul><li>MySQL</li><li>PostgreSQL</li><li>MariaDB</li><li>Microsoft SQL-Express</li><li>Microsoft SQL-We</li></ul> | <p></p><ul><li>Microsoft SQL-Standard</li><li>Aurora MySQL</li><li>Aurora MySQL Serverless</li><li>Aurora PostgreSQL</li><li>Aurora PostgreSQL Serverless</li></ul> |
| ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

\*Support for Aurora Serverless V1 database engines has been deprecated. Do not create V1 engines when using Terraform.

{% hint style="info" %}
When upgrading RDS versions, use the AWS Console and see your Cloud Provider for compatibility requirements. Note that while versions 5.7.40, 5.7.41, and 5.7.42 cannot be upgraded to version 8.0.28, you can upgrade them to version 8.0.32 and higher.
{% endhint %}

## Creating an RDS database <a href="#id-0-toc-title" id="id-0-toc-title"></a>

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database**.
2.  Click **Add**. The **Create a RDS** page displays.<br>

    <figure><img src="../../../../../.gitbook/assets/RDS create.png" alt=""><figcaption><p>The <strong>Create a RDS</strong> page in the DuploCloud Portal</p></figcaption></figure>
3. Complete the following fields:
   * **RDS Name**: Enter a unique name for the RDS instance. DuploCloud suggests using the Tenant name as a prefix, e.g., `tenantname-db`_._
   * **Create from Snapshot (Optional)**: Select an existing snapshot to restore from if applicable.
   * **RDS Engine**: Choose the database engine (e.g., MySQL, PostgreSQL, MariaDB).
   * **RDS Engine Version**: Select the engine version.
   * **Encryption Key (Optional)**: Select an encryption key if needed for encryption at rest.
   * **Storage Type (Optional)**: Choose the storage type (e.g., General Purpose SSD, Provisioned IOPS).
   * **Storage Size in GB** **(Optional)**: Specify the storage size in GiB. _(Minimum: 20 GiB, Maximum: 65,536 GiB.)_
   * **RDS Instance Size**: Choose an instance type based on performance needs.
   * **DB Parameter Group (Optional)**: Select a custom database parameter group if needed.
   * **DB Subnet Group (Optional)**: Choose a subnet group for the database network configuration.
   * **Backup Retention Period in Days**: Enter a retention period between **1 and 35** days.
   * **User Name**: Enter the database username. (Required)
   * **User Password**: Enter a secure password for the database. (Required)
   * Optionally, select **Enable Performance Insights.**
   * **Performance Insights Retention in Days (Optional)**: Enter the retention period for Performance Insights data. (Default: 7 days, Maximum: 731 days.)
   * **Performance Insights Encryption (Optional)**: Select an encryption key for encrypting Performance Insights data. (If not specified, AWS will use the default key.)
   * **Enable Additional Features (Optional):**
     * **Enable IAM Auth**
     * **Store Credentials in Secrets Manager**
     * **Enable Multi-AZ**
     * **Enable Logging**
4. Click **Create** to provision the RDS database.

## Creating an Aurora Serverless V2 Cluster database

You can create Aurora Serverless V2 Databases by selecting **Aurora-MySql-Serverless-V2** or **Aurora-PostgreSql-Serverless-V2** from the **RDS Database Engine** list box. Select the **RDS Engine Version** compatible with Aurora Serverless v2. The **RDS Instance Size** of `db.serverless` applies to both engines.

## Creating Aurora databases

### **Create Aurora Serverless V2 Cluster Database**

You can create Aurora Serverless V2 Databases by selecting **Aurora-MySQL-Serverless-V2** or **Aurora-PostgreSQL-Serverless-V2** from the **RDS Engine** list box. Select the RDS Engine Version compatible with Aurora Serverless v2. The **db.serverless** RDS Instance Size applies to both engines.

### **Storage Type Selection for Aurora**

When creating an **Aurora MySQL** or **Aurora PostgreSQL** database, you can select between two storage types:

* **Aurora** (standard storage type for Aurora databases).
* **aurora-iopt1** (optimized for high IOPS performance and low-latency disk operations, ideal for performance-intensive applications).

### Creating a publicly available RDS database

1. [Create a DB subnet group in AWS](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/SubnetGroups.Creating.html) consisting **only** of public subnets from your VPC.
2. &#x20;In the DuploCloud Portal, navigate to **Cloud Services** -> **Databases**
3. Select the **RDS** tab, and click **Add**. The **Create a RDS** page displays.&#x20;
4. In the **DB Subnet Group** list box select the public DB subnet group you created in AWS.&#x20;
5. Complete the remaining fields according to your requirements.&#x20;
6. Click **Create**. The publicly available RDS database is created.&#x20;

To create a public RDS database, you much first [create a DB subnet group in AWS](https://docs.aws.amazon.com/AmazonElastiCache/latest/dg/SubnetGroups.Creating.html) consisting only of public subnets from your VPC. Then follow the steps above to create an RDS database, selecting the DB subnet group you created from the DB Subnet Group list box.&#x20;

{% hint style="warning" %}
The DB subnet group created in AWS must **only** contain public subnets from your VPC. This configuration is crucial for making the database public.
{% endhint %}

## Connecting to the database <a href="#id-1-toc-title" id="id-1-toc-title"></a>

Once you create the database, select it and use the **Instances** tab to view the endpoint and credentials. Use the **Endpoints** and credentials to connect to the database from your application running in an EC2 instance. The database is only accessible from inside the EC2 instance in the current Tenant, including the containers running within.

For databases you intend to make publicly available, ensure proper security measures, including broad accessibility, are in place to protect your data.

<figure><img src="../../../../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.19-17_18_36.png" alt=""><figcaption><p>The <strong>Instances</strong> tab on the <strong>RDS</strong> details page</p></figcaption></figure>

{% hint style="info" %}
Pass the endpoint, name, and credentials to your application [using environment variables](../../containers/passing-config-and-secrets.md) for maximum security.
{% endhint %}

## Updating performance insights for an existing RDS

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database** and select the **RDS** tab.&#x20;
2. Click on the RDS name in the **NAME** column.
3. From the **Actions** menu, select **RDS Settings** and then **Update Performance Insights**. The **Update Performance Insights** pane displays.&#x20;
4. Select **Enable Performance Insights**.
5. In the **Performance Insights Retention in Days field**, enter a retention period (1–731 days).
6. From the **Performance Insights Encryption** list box, select an encryption key or select **No Encryption**.
7. **Click Update** to apply the changes.&#x20;

## Managing RDS Certificate Authorities

You can manage the Certificate Authority (CA) for an RDS instance when creating a new RDS database or by updating the CA for an existing database.

### **Choosing a Certificate Authority When Creating an RDS Database**

During the RDS creation process, select a **Certificate Authority** from a dropdown menu.

This option ensures that the RDS instance is set up with the correct certificate authority to encrypt communications using SSL/TLS. The selected CA will validate certificates to ensure secure and trusted connections.

### **Updating the Certificate Authority for an Existing RDS Database**

If you need to update the Certificate Authority used by an existing RDS database, you can do so through the **Actions** menu in the RDS instance settings:

1. Navigate to **Cloud Services** → **Databases**.
2. Select the **RDS** tab.
3. Select the RDS you want to modify from the **NAME** column.
4. From the **Actions** menu, choose **RDS Settings**.
5. Click **Update Certificate Authority**.
6. In the **Certificate Authority** list box, select the new CA to use for the instance.
7. Click **Save** to apply the new CA.
