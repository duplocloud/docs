# Sharing encrypted database

## Introduction <a href="#0-toc-title" id="0-toc-title"></a>

Sharing unencrypted database to other accounts is very simple and straightforward. But sharing an encrypted database is slightly difficult. Here we will go through the steps that needs to be followed to share the encrypted database.

## Step 1: Create a managed key <a href="#1-toc-title" id="1-toc-title"></a>

Create a new customer managed key in AWS KMS, in the define key usage permissions area provide the account id of the other account.

![](https://duplocloud.com/wp-content/uploads/2021/11/KMS-other-account.png)

## Step 2: Copy and share a snapshot <a href="#2-toc-title" id="2-toc-title"></a>

Once the key is created, go to **RDS > Snapshots**, select the snapshot and click Copy Snapshot. In the encryption change the master key to the key we created before.

![](https://duplocloud.com/wp-content/uploads/2021/11/KMS-copy-snapshot.png)

Once the copied snapshot is ready, as usual share the snapshot to another account by clicking share snapshot and providing the other account id.

## Step 3: Copy the shared snapshot <a href="#3-toc-title" id="3-toc-title"></a>

Now go to the other **AWS account > RDS > Shared with me**. Select the shared snapshot and click copy-snapshot again and change the encryption key to the encryption key in the account.

![](https://duplocloud.com/wp-content/uploads/2021/11/RDS-copysnapshot.png)

## Step 4: Add tags to the copied snapshot <a href="#4-toc-title" id="4-toc-title"></a>

In the copied snapshot add a tag with Key as “`Name`” and Value as “`duploservices-{tenantname}`” where `tenantname` is the tenant where u want to launch an RDS with this snapshot.

![](https://duplocloud.com/wp-content/uploads/2021/11/RDS-customtag.png)

## Step 5: Create a new database <a href="#5-toc-title" id="5-toc-title"></a>

Go to DuploCloud portal select the tenant. **Open RDS > Add new DB (+ icon) > Give** name for the new database. In the snapshot select the new snapshot. Enter instance type and hit submit. In few mins, the database will be created with the data from the snapshot. You must use the existing username and password to access the database.

![](<../../../../.gitbook/assets/Screen Shot 2022-07-08 at 11.58.39 AM.png>)
