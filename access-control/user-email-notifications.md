---
description: Configure new-user email notifications in DuploCloud
---

# User Email Notifications

DuploCloud supports system-generated email notifications for key user events, including welcome emails sent to new users when they're added to the system, and notification emails sent to specified recipients when a new admin user is added. This page explains how you to customize new user welcome emails, and configure new admin user emails.

## Customizing Welcome Emails for New Users

When a new user is added in DuploCloud, the system sends a welcome email. Complete the following steps to customize the email content.

1. Navigate to **Administrator** → **System Settings** → **System Config**.
2. Click **Add**. The **Add Config** pane displays.
3. In the **Config Type** list box, select **AppConfig**.&#x20;
4. In the **Key** field, select one of the following:&#x20;
   * `new_user_email_subject` : to customize the **subject line**
   * `new_user_email_body` :  to customize the **email body**
5. In the **Value** field, enter:
   * A **plain text** subject line (e.g., `Welcome to DuploCloud!`), or
   * An **HTML-formatted** email body (see example and formatting guidelines below).
6. Click **Submit**. The email subject line or body is customized.&#x20;

**Example Email Body:**

```html
Welcome to DuploCloud!<br /><br />
Your account has been created.<br /><br />
Username: {{username}}<br />
Login URL: {{env}}<br /><br />
Please reach out if you need help getting started.
```

{% hint style="info" %}
**Formatting Guidelines:**\
The **email subject** is plain text.\
The **email body** must be an **HTML-formatted string**.&#x20;

* Use `<br />` for line breaks.
* Use `&nbsp;` for extra spaces.
* Placeholders like `{{username}}` and `{{env}}` will be automatically filled in.
{% endhint %}

## **Configuring New Admin User Email Notifications**&#x20;

When a new admin user is created in DuploCloud, you can configure the system to send an email notification for added visibility. This is especially useful for auditing and compliance purposes. To configure new admin user email notifications, first enable new admin notifications, and then choose the notification recipients.&#x20;

### **Enabling New Admin User Email Notifications**&#x20;

1. Navigate to **Administrator** -> **System Settings** -> **System Config**.
2.  Click **Add**. The **Add Config** pane displays.\


    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (379).png" alt="" width="343"><figcaption><p>The <strong>Add Config</strong> pane</p></figcaption></figure></div>
3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="150.888916015625"></th><th></th></tr></thead><tbody><tr><td><strong>Config Type</strong></td><td>Select <strong>Flags</strong></td></tr><tr><td><strong>Key</strong></td><td>Select <strong>Enable new admin notification</strong></td></tr><tr><td><strong>Value</strong></td><td>Enter <code>True</code> to enable email notifications for new admin users.</td></tr></tbody></table>

4. Click **Submit** to save the setting. When the flag is set to `True`, an email will be sent to configured recipients (see steps below for configuring recipients) each time a new admin user is added.&#x20;

### Configuring New Admin Email Recipients

Configure which email addresses receive new admin user email notifications.

1. Navigate to **Administrator** → **System Settings** → **System Config**.
2.  Click **Add**. The **Add Config** pane displays.\


    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (469).png" alt="" width="340"><figcaption><p>The <strong>Add Config</strong> pane</p></figcaption></figure></div>
3. Complete the following fields:

<table data-header-hidden><thead><tr><th width="150.888916015625"></th><th></th></tr></thead><tbody><tr><td><strong>Config Type</strong></td><td>Select <strong>AppConfig</strong></td></tr><tr><td><strong>Key</strong></td><td>Select <strong>Notification Admin Emails</strong></td></tr><tr><td><strong>Value</strong></td><td>Enter one or more email addresses, separated by semicolons (e.g., <code>admin1@example.com;admin2@example.com</code></td></tr></tbody></table>

4. Click **Submit** to save the setting. It may take up to **24 hours** for the change to take effect. Once applied, the specified recipients will receive an email notification each time a new admin user is added.

{% hint style="warning" %}
Be careful when changing this setting, as it impacts who receives sensitive system notifications.
{% endhint %}
