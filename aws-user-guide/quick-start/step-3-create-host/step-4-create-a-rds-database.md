# Step 4: Create a RDS database

## Create a database <a href="#0-toc-title" id="0-toc-title"></a>

Create a MySQL, Microsoft SQL, PostgreSQL or Amazon Aurora database from the menu **DevOps** > **Database** > **Relational Databases** > **+Add** button above the table.

![](https://duplocloud.com/wp-content/uploads/2021/11/createrds.png)

{% hint style="info" %}
Keep an eye on the faults that may show up on the top right. If there is a fault click on it and see if it is due to DB creation failure. Common cases for these are passwords cannot have special characters like quotes, @, comma. Choosing encryption for small instances like micro, small and medium&#x20;
{% endhint %}

## Connect to the database <a href="#1-toc-title" id="1-toc-title"></a>

Once the database is created which takes about 5 to 10 mins then you can expand the created database to fetch the endpoint and credentials. Use this endpoint and credentials to connect to the database from your application running in the EC2 instance. Note that the database is only accessible from inside the EC2 instance (including the containers running within it) in the current tenant.

![](https://duplocloud.com/wp-content/uploads/2021/11/rdsdetails.png)

{% hint style="info" %}
The easier way to pass DB endpoint, name and credentials to your application for security purposes is through environment variables (`ENV`) of the Service. Other was are passing via secrets manager or Kubernetes secrets
{% endhint %}
