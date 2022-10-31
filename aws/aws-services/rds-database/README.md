# RDS database

## Create a database <a href="#0-toc-title" id="0-toc-title"></a>

Create a MySQL, Microsoft SQL, PostgreSQL or Amazon Aurora database from the menu **DevOps** > **Database** > **RDS** > **+Add** button above the table.\


![](<../../../.gitbook/assets/image (38) (2).png>)

#### Create Aurora Serverless V2 Cluster database

User can create Aurora Serverless V2 Database by selecting RDS Database Engine as Aurora-MySQL/Postgres. Select the RDS Engine Version that's compatible with Aurora Serverless v2.

Select **RDS Instance Size** as \`db.serverless\`

## Connect to the database <a href="#1-toc-title" id="1-toc-title"></a>

Once the database is created which takes about 5 to 10 mins then you can expand the created database to fetch the endpoint and credentials. Use this endpoint and credentials to connect to the database from your application running in the EC2 instance. Note that the database is only accessible from inside the EC2 instance (including the containers running within it) in the current tenant.

![](https://duplocloud.com/wp-content/uploads/2021/11/rdsdetails.png)

{% hint style="info" %}
The best way to pass DB endpoint, name and credentials to your application for security purposes is through environment variables (`ENV`) of the Service.
{% endhint %}
