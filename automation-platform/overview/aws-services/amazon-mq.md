# Amazon MQ

DuploCloud supports [Amazon MQ](https://aws.amazon.com/amazon-mq/features/#topic-0), a fully managed message broker service for [Apache ActiveMQ](https://activemq.apache.org/) and [RabbitMQ](https://www.rabbitmq.com/). You can use Amazon MQ to enable asynchronous communication between different parts of your application or between microservices. Through the DuploCloud Portal, you can easily create and manage Amazon MQ brokers and configurations.&#x20;

## Creating a Broker Configuration

Broker configurations define reusable settings for RabbitMQ and ActiveMQ brokers and can be attached to one or more brokers.

1. Navigate to **Cloud Services** → **App Integration** → **Amazon MQ**.
2. Select the **Configurations** tab.
3.  Click **Add**. The **Create Configuration** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (745).png" alt=""><figcaption><p><strong>Create Configuration</strong> pane</p></figcaption></figure></div>
4. Complete the following fields:

<table data-header-hidden><thead><tr><th width="205.111083984375">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Configuration Name</strong></td><td>Enter a descriptive name for the configuration.</td></tr><tr><td><strong>Broker Engine Type</strong></td><td>Select <strong>RabbitMQ</strong> or <strong>Apache ActiveMQ</strong>.</td></tr><tr><td><strong>Broker Engine Version</strong></td><td>Select the version of the chosen broker engine, e.g., <strong>3.13</strong>.</td></tr><tr><td><strong>Authentication Type</strong></td><td>For Apache ActiveMQ brokers, choose <strong>Simple</strong> or <strong>LDAP</strong> authentication type.</td></tr></tbody></table>

5. Click **Create** to create the broker configuration.

## Managing Broker Configurations

Once a configuration is created, you can view or manage it from the **Configurations** tab:

1. Navigate to **Cloud Services** → **App Integration** → **Amazon MQ**.
2. Select the **Configurations** tab.
3. Select the configuration you want to manage from  the **NAME** column.
4. Choose from the following tabs to view configuration details:

<table data-header-hidden><thead><tr><th width="209.55548095703125"></th><th></th></tr></thead><tbody><tr><td><strong>Configuration Details</strong></td><td>Displays the XML configuration.</td></tr><tr><td><strong>Revisions</strong></td><td>Shows a history of changes made to the configuration.</td></tr><tr><td><strong>Tags</strong></td><td>Displays tags applied to the Amazon MQ configuration, such as project, lifecycle, and tenant identifiers.</td></tr><tr><td><strong>JSON Details</strong></td><td>Displays metadata and revision information about the Amazon MQ configuration in JSON format.</td></tr></tbody></table>

<div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (754).png" alt=""><figcaption><p> <strong>Configuration Details</strong> tab on the configuration details page</p></figcaption></figure></div>

## Revising a Broker Configuration

To revise a preexisting broker configuration:&#x20;

1.  In the **Configuration Details** tab, click **Edit** to update the configuration.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (759).png" alt=""><figcaption><p> <strong>Configuration Details</strong> tab showing broker configuration revision process</p></figcaption></figure></div>
2. Optionally, add a **Description** for the revision.
3. Modify the configuration values as needed.
4. Click **Save** to apply the revision. All revisions are listed on the **Revisions** tab.

## Creating a RabbitMQ Broker

DuploCloud allows you to create RabbitMQ brokers to handle messaging workloads. You can optionally attach a previously created broker configuration to reuse settings like engine type, version, and authentication mode.

1. Navigate to **Cloud Services** → **App Integration** → **Amazon MQ**.
2. Select the **Brokers** tab.
3.  Click **Add**. The **Add Broker** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (748).png" alt=""><figcaption><p><strong>Add Broker</strong> pane</p></figcaption></figure></div>
4. Complete the required fields:

<table data-header-hidden><thead><tr><th width="211.33331298828125">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Broker Name</strong></td><td>Enter a unique name for your broker.</td></tr><tr><td><strong>Broker Engine Type</strong></td><td>Select <strong>RabbitMQ</strong>.</td></tr><tr><td><strong>Broker Engine Version</strong></td><td>Choose the ActiveMQ engine version, e.g., <strong>3.13</strong>.</td></tr><tr><td><strong>Username</strong></td><td>Enter the username for broker access.</td></tr><tr><td><strong>Password</strong></td><td>Enter the password for the username.</td></tr></tbody></table>

5. Optionally, select **Advanced Options** and configure the following advanced configurations.

<table data-header-hidden><thead><tr><th width="218.4444580078125">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Broker Configuration</strong></td><td>Select a previously created broker configuration. For more details, see <a href="amazon-mq.md#creating-a-broker-configuration">Creating a Broker Configuration</a>. </td></tr><tr><td><strong>CloudWatch Logs</strong></td><td>Select to enable general logging via CloudWatch.</td></tr><tr><td><strong>Public Network Access</strong></td><td>Select to enable connections from applications outside of the VPC that hosts the broker's subnets.</td></tr><tr><td><strong>Subnet(s)</strong></td><td>If public network access is not enabled, select one or more subnets where the broker will be deployed. </td></tr><tr><td><strong>Encryption</strong></td><td>Choose encryption settings (e.g., <strong>AWS managed CMK</strong>).</td></tr><tr><td><strong>Maintenance Window</strong></td><td>Select this option to define a maintenance window for broker updates.</td></tr></tbody></table>

6. Click **Submit** to create the broker.

<div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (749).png" alt=""><figcaption><p><strong>Brokers</strong> list on the <strong>Amazon MQ</strong> tab</p></figcaption></figure></div>

## Creating an ActiveMQ Broker

DuploCloud supports provisioning and managing ActiveMQ brokers to enable communication between distributed applications.

1. Navigate to **Cloud Services** → **App Integration** → **Amazon MQ**.
2. Select the **Brokers** tab.
3. Click **Add**. The **Add Broker** pane displays.

<div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (750).png" alt=""><figcaption><p><strong>Add Broker</strong> page </p></figcaption></figure></div>

4. Complete the following fields:

<table data-header-hidden><thead><tr><th width="230.88885498046875">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Broker Name</strong></td><td>Enter a unique name for your ActiveMQ broker.</td></tr><tr><td><strong>Broker Engine Type</strong></td><td>Select <strong>Apache ActiveMQ</strong>.</td></tr><tr><td><strong>Broker Engine Version</strong></td><td>Choose the ActiveMQ engine version to use, e.g., <strong>5.18</strong>.</td></tr><tr><td><strong>Deployment Mode</strong></td><td>Select the deployment mode (e.g., <strong>Single Instance Broker</strong>).</td></tr><tr><td><strong>Storage Type</strong></td><td>Choose the storage type (e.g., <strong>EBS - Throughput Optimized</strong>).</td></tr><tr><td><strong>Broker Instance Type</strong></td><td>Select the broker instance type.</td></tr><tr><td><strong>ActiveMQ Access</strong></td><td><p>Choose the authentication method for the broker and provide additional information:</p><ul><li><strong>Simple:</strong> Provide a username and password to authenticate directly with the broker.</li><li><strong>LDAP:</strong> Provide LDAP connection details so the broker can authenticate users against your corporate directory. </li></ul></td></tr></tbody></table>

5. Optionally, select **Advanced Options** and complete the fields, organized by category in the table below.

<table data-header-hidden><thead><tr><th width="214.88885498046875"></th><th></th></tr></thead><tbody><tr><td><strong>Broker Configuration</strong></td><td>Select a previously created broker configuration. For more details, see <a href="amazon-mq.md#creating-a-broker-configuration">Creating a Broker Configuration</a>. </td></tr><tr><td><strong>Monitoring</strong></td><td>Enable <strong>CloudWatch General Logs</strong> and/or <strong>CloudWatch Audit Logs</strong>.</td></tr><tr><td><strong>Network Settings</strong></td><td>Enable or disable <strong>Public Network Access</strong> and select one or more <strong>Subnets</strong> in which to launch the broker.</td></tr><tr><td><strong>Data Encryption</strong></td><td>Choose encryption options for broker data, e.g., <strong>AWS owned CMK</strong>.</td></tr><tr><td><strong>Maintenance Window</strong></td><td>Select this option to define a maintenance window for broker updates.</td></tr></tbody></table>

6. Click **Submit** to create the broker.

<div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (752).png" alt=""><figcaption><p><strong>Brokers</strong> list on the <strong>Amazon MQ</strong> tab</p></figcaption></figure></div>

## Managing a Broker

After creating a broker, you can view its details, monitor its status, and perform management actions from the DuploCloud portal.

1. Navigate to **Cloud Services** → **App Integration** → **Amazon MQ**.
2. Select the **Brokers** tab.
3. Click the broker name in the **NAME** column.
4. Choose from the following tabs to view or manage the broker:

<table data-header-hidden><thead><tr><th width="170.22222900390625">Tab</th><th>Description</th></tr></thead><tbody><tr><td><strong>Details</strong></td><td>Displays key broker specifications, security, logging, encryption, and maintenance settings in a human-readable format.</td></tr><tr><td><strong>Tags</strong></td><td>Displays system-generated and user-defined tags applied to the Amazon MQ broker, such as project, lifecycle, and tenant identifiers.</td></tr><tr><td><strong>JSON Details</strong></td><td>Shows the full Amazon MQ broker configuration in raw JSON format, including deployment, network, and engine settings.</td></tr></tbody></table>

<div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (757).png" alt=""><figcaption><p><strong>JSON Details</strong> tab on the broker's details page</p></figcaption></figure></div>

5. If needed, click **Actions** to **Edit** or permanently **Delete** the broker.

<div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (766).png" alt=""><figcaption><p>Broker details page with <strong>Actions</strong> highlighted</p></figcaption></figure></div>
