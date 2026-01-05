# Aurora Global Database

DuploCloud supports [Aurora Global Database](https://aws.amazon.com/rds/aurora/global-database/), a multi-region Aurora database that lets applications read from local copies if a region goes down. This setup improves application performance for global audiences and helps maintain availability during regional outages.

## Creating the Primary Aurora Cluster

1. In the DuploCloud Portal, navigate to **Cloud Services** → **Database.**
2.  Select the **RDS** tab, and click **Add**. The **Create a RDS** pane displays. <br>

    <figure><img src="../../../../../.gitbook/assets/Screenshot (834).png" alt=""><figcaption><p><strong>Create a RDS</strong> pane</p></figcaption></figure>
3. Complete the required fields:

<table data-header-hidden><thead><tr><th width="205.11114501953125"></th><th></th></tr></thead><tbody><tr><td><strong>RDS Name</strong></td><td>Enter a unique name for the primary cluster.</td></tr><tr><td><strong>RDS Engine</strong></td><td>Select <strong>Aurora MySQL</strong> or <strong>Aurora PostgreSQL</strong>.</td></tr><tr><td><strong>RDS Engine Version</strong></td><td><p>Select a compatible version that supports Global Aurora:<br></p><ul><li><strong>Aurora MySQL</strong>: 5.7+ or 8.0+</li><li><strong>Aurora PostgreSQL</strong>: 11+</li></ul></td></tr><tr><td><strong>RDS Instance Size</strong></td><td>Select a supported instance size for Global Aurora (<strong>db.r5</strong> or higher).</td></tr><tr><td><strong>User Name</strong></td><td>Enter the username for the cluster administrator.</td></tr><tr><td><strong>User Password</strong></td><td>Enter a password for the cluster administrator.</td></tr></tbody></table>

4. Complete any other optional fields to configure your database according to your needs (see the [RDS database](../../../../../aws-user-guide/aws-services/database/rds-database/) page for optional field descriptions).
5. Click **Create** to provision the primary cluster. Allow 5–10 minutes for it to become available

## Adding a Secondary Region to Create a Global Aurora Cluster

1. Navigate to **Cloud Services** → **Database**.
2. Select the **RDS** tab.
3. Select the primary Aurora cluster you previously created in the **NAME** column.
4.  Click **Actions** → **RDS Settings** → **Add Region**. The **Add Region** pane displays.<br>

    <div align="left"><figure><img src="../../../../../.gitbook/assets/Screenshot (836).png" alt=""><figcaption><p><strong>Add Region</strong> pane</p></figcaption></figure></div>
5. Complete the following fields:

<table data-header-hidden><thead><tr><th width="232.66656494140625"></th><th></th></tr></thead><tbody><tr><td><strong>Global Cluster Name</strong></td><td>Enter a custom name for the global cluster name by adding a suffix or unique identifier. Do not remove or change the prefix. Each Aurora cluster can belong to only one Global Aurora cluster. Global cluster names must be unique within your account/region. Attempting to add a cluster to multiple global clusters will fail.</td></tr><tr><td><strong>Tenant</strong></td><td>Select the tenant in the secondary region where the read-only cluster will be created.</td></tr><tr><td><strong>Secondary Cluster Name</strong></td><td>Enter a unique name for the secondary (read-only) cluster by adding a suffix or unique identifier. Do not remove or change the prefix.</td></tr></tbody></table>

6. Click **Update** to provision the secondary cluster.
7. Once the secondary cluster is created, allow up to 40 minutes for it to become available, then follow the steps under **Viewing a Global Cluster** to verify the global setup.

## Viewing a Global Cluster

1. Navigate to **Cloud Services** → **Database.**
2. Select the **RDS** tab.
3. Select the the cluster you wish to view from the **NAME** column.&#x20;
4. Select the **Global Cluster** tab. For each cluster in the global setup, the following information is shown:

<table data-header-hidden><thead><tr><th width="171.11114501953125">Column</th><th>Description</th></tr></thead><tbody><tr><td><strong>Cluster Name</strong></td><td>The name of the cluster.</td></tr><tr><td><strong>Region</strong></td><td>The AWS region where the cluster resides</td></tr><tr><td><strong>Role</strong></td><td>Indicates whether the cluster is the <strong>Primary</strong> (write) or <strong>Secondary</strong> (read-only replica)</td></tr><tr><td><strong>Status</strong></td><td>The current status of the cluster (e.g., <strong>Available</strong>, <strong>Created</strong>)</td></tr></tbody></table>

## Accessing Aurora Cluster Endpoints

Each cluster in a global Aurora setup has a specific role: the primary cluster handles all writes, and secondary clusters handle reads in their respective regions. Follow the steps below to connect to each type of cluster.

### Connecting to the Primary Cluster

1. Select the appropriate tenant, go to **Cloud Services** → **Database** → **RDS**, and click on the primary cluster name.
2. Copy the **Writer** endpoint.
3. Use this endpoint for all write operations (`INSERT`, `UPDATE`, `DELETE`).

<figure><img src="../../../../../.gitbook/assets/Screenshot (837).png" alt=""><figcaption><p>RDS details page for the primary Aurora database with the Writer endpoint highlighted</p></figcaption></figure>

### Connecting to Secondary Clusters

Each secondary cluster in a different region has its own reader endpoint.

1. Select the appropriate tenant, go to **Cloud Services** → **Database** → **RDS**, and click on the secondary cluster name.
2. Copy the **Reader** endpoint for that cluster.
3. Use this endpoint for all read operations (`SELECT` queries) in that region.
