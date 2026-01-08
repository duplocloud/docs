# AWS DynamoDB database

When using DynamoDB in DuploCloud AWS, the required permissions to access the DynamoDB from a virtual machine (VM), Lambda functions, and containers are provisioned automatically using Instance profiles. Therefore, no Access Key is required in the Application code.

{% hint style="warning" %}
When you write application code for DynamoDB in DuploCloud AWS, use the IAM role/Instance profile to connect to these services. If possible, use the AWS SDK constructor, which uses the region.
{% endhint %}

## Adding DynamoDB Database Tables

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database.**
2. Select the **DynamoDB** tab.
3.  Click **Add**. The **Create DynamoDB** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (775).png" alt=""><figcaption><p>The <strong>Create DynamoDB</strong> pane<br></p></figcaption></figure></div>
4. Complete the following fields:

<table data-header-hidden><thead><tr><th width="228.2222900390625"></th><th></th></tr></thead><tbody><tr><td><strong>Table Name</strong></td><td>Enter a name for the table.</td></tr><tr><td><strong>Primary Key</strong></td><td>Enter the primary key.</td></tr><tr><td><strong>Data Type</strong> <em>(Primary Key)</em></td><td>Select the data type for the primary key (<strong>String</strong> or <strong>Number</strong>).</td></tr><tr><td><strong>Sort Key</strong></td><td>Enter the sort key.</td></tr><tr><td><strong>Data Type</strong> <em>(Sort Key)</em></td><td>Select the data type for the sort key (<strong>String</strong> or <strong>Number</strong>).</td></tr><tr><td><strong>Secondary Indexes</strong></td><td>To add a secondary index, click <strong>Add Local Index</strong> and specify the following:<br>• <strong>Sort Key</strong>: Enter the attribute used to sort items within the partition.<br>• <strong>Data Type</strong>: Select the data type of the sort key (e.g., String, Number).<br>• <strong>Index Name</strong>: Enter a unique name for the secondary index.<br>• <strong>Projection</strong>: Specify which attributes to include in the index (e.g., <strong>All</strong>, <strong>Only Keys</strong>, or <strong>Include</strong> and enter a specific attribute).</td></tr></tbody></table>

5. Click **Submit**.&#x20;

For detailed guidance about configuring the `duplocloud_aws_dynamodb_table`, refer to the Terraform[ documentation](https://registry.terraform.io/providers/duplocloud/duplocloud/latest/docs/resources/aws_dynamodb_table). This resource allows for creating and managing AWS DynamoDB tables within DuploCloud.

{% hint style="info" %}
Perform additional configuration, as needed, in the AWS Console by clicking the   **>\_** **Console** icon. In the AWS console, you can configure the application-specific details of DynamoDB database tables. However, no access or security-level permissions are provided.
{% endhint %}

After creating a DynamoDB table, you can retrieve the final name of the table using the `.fullname` attribute, which is available in the read-only section of the documentation. This feature is handy for applications that dynamically access table names post-creation. If you encounter any issues or need further assistance, please refer to the documentation or contact support.
