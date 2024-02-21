# API tokens

## Introduction

Duplo supports two kinds of API tokens, temporary API tokens and permanent API tokens. For normal use cases, we recommend using a temporary API token. For CI/CD or other DevOps automation, a permanent API token is warranted.

{% hint style="warning" %}
Permanent API tokens will expire after one year.
{% endhint %}

## Temporary API tokens

Every time a user logs in to Duplo, a temporary API token is created for that user that only lasts for the duration of their session.

### Getting a Temporary API token

Any user can retrieve _their own_ temporary API token from Duplo. Navigate to the **User** -> **Profile** page. Click the copy icon ![](<../../.gitbook/assets/Screen Shot 2022-02-24 at 2.19.23 PM.png>) in the **Temporary API Token** pane.

<figure><img src="broken-reference" alt=""><figcaption></figcaption></figure>

## Permanent API tokens

Only administrators can create permanent API tokens. Permanent tokens are always associated with a specific Duplo user.

{% hint style="warning" %}
**Note:** Permanent API tokens will expire after one year.
{% endhint %}

### Creating a permanent API token

Navigate to the **Administrator -> Users** page. Click the username in the list, to go to a specific user's page. Click the **Tokens** tab.

<figure><img src="broken-reference" alt=""><figcaption></figcaption></figure>

Click the blue **+ Add** button. Give your token a memorable name and click **Create**.

<div align="left">

<img src="../../.gitbook/assets/Screen Shot 2022-02-24 at 2.27.12 PM.png" alt="">

</div>

Click the **Copy** button to copy your token to the clipboard. Save it somewhere safe, you will not be able to retrieve it from Duplo later.

![](<../../.gitbook/assets/Screen Shot 2022-02-24 at 2.29.53 PM.png>)

{% hint style="danger" %}
**Caution:** Always save your token somewhere safe. You will not be able to retrieve it again from Duplo after you have created it. However, if you lose your token, you can always create a new one.
{% endhint %}

### Configuring notifications for API tokens nearing expiration

You can configure DuploCloud system settings to generate faults and send notification emails when API tokens are nearing expiration.

#### **Generate a fault when API tokens are near expiration:**

1. From the DuploCloud portal, navigate to **Administrator** -> **Systems Settings**. Select the **Config** tab, and click **Add.**&#x20;
2. For **Config Type** select **App Config**, for **Key**, select **Enable User Token Notification**, and in the **Value** field, enter the **number of days** before token expiration when faults should show.&#x20;

<div align="left">

<figure><img src="../../.gitbook/assets/image (4) (7).png" alt=""><figcaption><p><strong>Add Config</strong> pane configured to generate faults when API tokens will expire in 15 days. </p></figcaption></figure>

</div>

3. Click **Submit**. DuploCloud will generate a fault when an API token is the set number of days from expiration.&#x20;

#### **Sending notification emails when API tokens are near expiration:**

1. From the DuploCloud portal, navigate to **Administrator** -> **Systems Settings**. Select the **Config** tab, and click **Add.**&#x20;
2.  For **Config Type** select **App Config**, for **Key**, select **User Token Expiration Notification Emails**, and in the **Value** field, enter the **user email addresses** (separated by semicolons) to which notification emails will be sent. \


    <div align="left">

    <figure><img src="../../.gitbook/assets/token ex email.png" alt=""><figcaption><p><strong>Add Config</strong> pane configured to send a notification email when API tokens will expire in 15 days. </p></figcaption></figure>

    </div>
3. Click **Submit**. DuploCloud will send an email to the listed email address(es) when an API token is the set number of days from expiration.

