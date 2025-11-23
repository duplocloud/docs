---
description: Adding SQL Databases in DuploCloud
---

# Cloud SQL

DuploCloud supports creating and managing Cloud SQL databases in Google Cloud Platform (GCP) through the DuploCloud Portal. You can provision **MySQL**, **PostgreSQL**, or **SQL Server** instances using preconfigured tiers or custom node types. This allows you to tailor your database setup for performance, cost, or compliance requirements including the ability to deploy dedicated PostgreSQL nodes using custom vCPU and memory settings.

## Creating a Cloud SQL database

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Cloud SQL**.
2.  Click **Add**. The **Add SQL DB** page displays. <br>

    <figure><img src="../../../../.gitbook/assets/Screenshot (843).png" alt=""><figcaption><p><strong>Add SQL DB</strong> page in the DuploCloud Portal</p></figcaption></figure>
3.  Complete the fields as required.

    <table data-header-hidden><thead><tr><th width="192"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a name for the Cloud SQL database. This will be used as the resource identifier.</td></tr><tr><td><strong>Edition</strong></td><td>Select from the supported Cloud SQL editions (<strong>Enterprise</strong> or <strong>Enterprise Plus</strong>)</td></tr><tr><td><strong>SQL Version</strong></td><td>Select the database engine and version to use (e.g., <strong>PostgreSQL 15</strong>, <strong>MySQL 8</strong>).</td></tr><tr><td><strong>Tier</strong></td><td>Select a predefined machine type (e.g., <strong>1 vCPU 3.75 GB</strong>) or choose <strong>Custom Node</strong> and specify a custom machine tier by entering it manually in the <strong>Other Tier</strong> field. Refer to <a href="https://cloud.google.com/sql/docs/postgres/instance-settings">GCP Instance Settings</a> to find valid tier names.</td></tr><tr><td><strong>Root Password</strong></td><td>Enter a password for the root/admin database user.</td></tr><tr><td><strong>No Password</strong></td><td>Enable to create the database without setting a root password. This is typically used when authentication will be managed through IAM or other external mechanisms.</td></tr><tr><td><strong>Disk Size (in GB)</strong></td><td>Enter the disk size for the Cloud SQL instance.</td></tr><tr><td><strong>Labels</strong></td><td>Optionally, add key-value pairs to organize or tag your database resources.</td></tr></tbody></table>
4. Click **Create**.&#x20;

## Viewing a Cloud SQL database

You can view database details and configure other options by navigating to **Cloud Services** ->  **Cloud SQL** and selecting the Cloud SQL database from the **NAME** column.

<figure><img src="../../../../.gitbook/assets/CloudSQL details.png" alt=""><figcaption><p>The Cloud SQL database details page in the DuploCloud Portal</p></figcaption></figure>

## Additional Supported Actions

1. Navigate to **Cloud Services** ->  **Cloud SQL.**
2. Click the menu icon ( <img src="https://docs.duplocloud.com/~gitbook/image?url=https%3A%2F%2F2471407984-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F68cb0s9ce5UIUKWPuYs8%252Fuploads%252F1bULWx4HFiK9TRFeLpk4%252FKabab_three_Vertical_dots.png%3Falt%3Dmedia%26token%3De0fb9551-05e2-4e66-ac2b-c50a23f66acc&#x26;width=20&#x26;dpr=4&#x26;quality=100&#x26;sign=d18bec42&#x26;sv=1" alt="" data-size="line"> ) on the left of the row listing your SQL database, and select **GCP Console**, **Edit**, **Delete**, **Stop**, **Restart**, or **Reset Password**.

## Retaining Backups Before Cloud SQL Deletion

This setting ensures that a backup is automatically taken and stored in a designated Storage Bucket in GCP before a Cloud SQL instance is deleted, providing a safeguard for data recovery.

1. When deleting a Cloud SQL instance, enable the **Retain backups** option to retain backups.

<div align="left"><figure><img src="../../../../.gitbook/assets/image (2) (6).png" alt=""><figcaption><p>The <strong>Delete SQL Database</strong> pane with <strong>Retain backups</strong> enabled</p></figcaption></figure></div>
