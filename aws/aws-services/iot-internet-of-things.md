---
description: Enabling IoT for a Tenant, creating Things and supporting certificates
---

# IoT (Internet of Things)

Connect and manage billions of devices with AWS IoT, per Tenant. Collect, store, and analyze IoT data for industrial, consumer, commercial, and automotive workloads within DuploCloud.

{% hint style="info" %}
Use [Just-In-Time access](../use-cases/jit-access.md) to provision devices in your IoT.
{% endhint %}

## Enabling IoT for a Tenant&#x20;

1. In the DuploCloud Portal, navigate to **Administrator** -> **Tenants**.
2. Select your Tenant in the **Name** column.
3. Click the **Settings** tab.
4.  Click **Add**. The **Add Tenant Feature** pane displays.

    <figure><img src="../../.gitbook/assets/AWS_IOT_Create.png" alt=""><figcaption><p><strong>Add Tenant Feature</strong> pane with <strong>Enable AWS IoT</strong> feature selected</p></figcaption></figure>
5. From the **Select Feature** list box, select **Enable AWS IoT** and **Enable**.
6. Click **Add**. It takes approximately five minutes to enable IoT.&#x20;
7.  Navigate to **DevOps** -> **IoT**.  The IoT **Things** page displays.

    <figure><img src="../../.gitbook/assets/IOT_things_page.png" alt=""><figcaption><p>IoT <strong>Things</strong> page</p></figcaption></figure>

## Creating IoT Things

1. In the DuploCloud Portal, navigate to **DevOps** -> **IoT**.
2. Click the **Things** tab.
3.  Click **Add**. The **Create an IoT Thing** pane displays.

    <figure><img src="../../.gitbook/assets/IOT_Create_Thing_Attr (1).png" alt=""><figcaption><p><strong>Create an IoT Thing</strong> pane with <strong>AttributesACtions</strong> </p></figcaption></figure>
4. In the editable portion of the **Name** field, enter a Thing name.&#x20;
5. From the **IoT Certificate** list box, select an IoT Certificate.
6. From the **IoT Thing Type** list box, select the Thing type that you want to create.
7. In the **Attributes** field, add Thing Attributes in quotes, separated by a comma (**,**).
8. Click **Create**. Your IoT Thing is created and displayed.&#x20;

Select the Thing to view **Details** and **IoT Principals** (certificate information) for the Thing. Use the **Action** menu to **Edit** or **Delete** the Thing, **Attach IoT Certificate**, and **Download Device Package**.

<figure><img src="../../.gitbook/assets/IOT_Details.png" alt=""><figcaption><p><strong>Details</strong> and <strong>IoT Principals</strong> tabs on IoT <strong>Things</strong> page</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/IOT_Actions.png" alt=""><figcaption><p><strong>Actions</strong> menu on IoT <strong>Things</strong> page</p></figcaption></figure>

## Attach a certificate to a Thing

1. In the DuploCloud Portal, navigate to **DevOps** -> **IoT**.
2. Click the **Things** tab.
3. [Add a certificate](iot-internet-of-things.md#adding-a-certificate) if needed.
4. Select the Thing to which you want to attach a certificate from the **Name** column.
5. Click the Actions menu and select **Attach IoT Certificate**. The **Attach an IoT Certificate** pane displays.
6. From the **IoT Certificate** list box, select an IoT certificate to attach to the Thing.
7. Click **Attach**.

## Download the Device Package for a Thing

1. In the DuploCloud Portal, navigate to **DevOps -> IoT**.&#x20;
2. Click the **Things** tab.&#x20;
3. Select the Thing to which you want to attach a certificate from the **Name** column.&#x20;
4.  Click the **Actions** menu and select **Download Device Package**. The **Download IoT Device Package** window displays.&#x20;

    <figure><img src="../../.gitbook/assets/IOT_Download.png" alt=""><figcaption></figcaption></figure>
5. From the **IoT Certificate** list box, select the IoT certificate associated with the Thing's Device Package.&#x20;
6. Click **Download**.

## Certificate management

Add, update, or manage an IoT certificate with the following procedures.

### Adding a certificate

1. In the DuploCloud Portal, navigate to **DevOps** -> **IoT**.
2. Click the **Certificates** tab.
3.  Click **Add**. The **Create an IoT Certificate** pane displays.

    <figure><img src="../../.gitbook/assets/IOT_create_cert.png" alt=""><figcaption><p><strong>Create an IoT Certificate</strong> pane</p></figcaption></figure>
4. Select **Activate the Certificate** and click **Create**. The certificate displays.&#x20;

### Updating a certificate

1. In the DuploCloud Portal, navigate to **DevOps** -> **IoT**.
2. Click the **Certificates** tab. The available certificates are displayed and listed by **ID**.
3.  In the row for the certificate you want to update, click the **Actions** menu ( <img src="../../.gitbook/assets/Kabab_three_Vertical_dots (3).png" alt="" data-size="line"> ) and select **Edit**. The **Update an IoT Certificate** pane displays.

    <figure><img src="../../.gitbook/assets/IOT_update_cert.png" alt=""><figcaption></figcaption></figure>
4. From the **Status** list box, select the new status of the certificate.
5. Click **Update**.

### Manage a certificate using AWS Console

1. In the DuploCloud Portal, navigate to **DevOps** -> **IoT**.
2. Click the **Certificates** tab. Available certificates are displayed and listed by **ID**.
3. In the row for the certificate you want to update, click the <img src="../../.gitbook/assets/Kabab_three_Vertical_dots (1) (1) (1).png" alt="" data-size="line"> icon in the **Actions** column.
4.  Select **Console**. The AWS Console launches so that you can manage your certificate using AWS.

    <figure><img src="../../.gitbook/assets/IOT_AWS_console.png" alt=""><figcaption><p>AWS Console for managing certificates</p></figcaption></figure>



## Using IoT Topic Rules

Topic Rules are SQL-based rules that select data from message payloads and send data to other services, such as Amazon S3, Amazon DynamoDB, and AWS Lambda. Define a Rule to invoke a Lambda function when invoking an AWS or third-party service.

To learn more about IoT Topic Rules and how you define and manage them, see the [AWS documentation](https://docs.aws.amazon.com/iot/latest/developerguide/iot-rules.html).

### Adding IoT Topic Rules

1. In the DuploCloud Portal, navigate to **DevOps -> IoT**.&#x20;
2. Click the **Topic Rules** tab.
3.  Click **Add**. The **Add** Topic Rules page displays.

    <figure><img src="../../.gitbook/assets/IOT_R_1.png" alt=""><figcaption><p><strong>Add</strong> Topic Rules page</p></figcaption></figure>
4. In the **Name** field, enter a Topic Rule name.
5. Add a meaningful description of what the rule does in the **Description** field.
6. Define the rule by completing the fields in the **AWS IoT SQL** and **AWS IoT SQL Version** areas. Select **Define an Error Action** if the rule pertains to error management.
7.  Click **Create**. Your rule is defined and displayed in the **Topic Rules** tab.

    <figure><img src="../../.gitbook/assets/IOT_R_2.png" alt=""><figcaption><p>An IoT Topic Rule in the <strong>Topic Rules</strong> tab</p></figcaption></figure>

### Viewing a Topic Rule

View the details of a rule by selecting the rule from the **Topic Rules** tab Name column. The **Details** tab displays the rule description. The **Actions** tab displays the SQL-based rule(s).

<figure><img src="../../.gitbook/assets/IOT_R_3.png" alt=""><figcaption><p>Topic Rule <strong>Details</strong> tab</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/IOT_R_4.png" alt=""><figcaption><p>Topic Rule <strong>Actions</strong> tab</p></figcaption></figure>

### Editing a Topic Rule

In the **Topic Rules** tab, edit a Topic Rule by clicking the **Actions** menu ( <img src="../../.gitbook/assets/Kabab_three_Vertical_dots (3).png" alt="" data-size="line"> ) in the row listing your Topic Rule **Name**, and selecting **Edit**.

<figure><img src="../../.gitbook/assets/AWS_IOT_Topic_Rule_Actions (1).png" alt=""><figcaption><p><strong>Actions</strong> menu with <strong>Edit</strong> option on <strong>Topic Rules</strong> tab</p></figcaption></figure>
