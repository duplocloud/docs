---
description: >-
  Create and manage secrets in AWS Secrets Manager directly from the DuploCloud
  Portal
---

# AWS Secrets Support

DuploCloud integrates with [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html), enabling you to securely store and reference sensitive data such as API keys, passwords, and tokens within your applications and infrastructure.

## Creating an AWS Secret

To create a new secret in AWS Secrets Manager from the DuploCloud Portal:

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **App Integration**.
2. Select the **AWS Secrets** tab.
3.  Click **Add**. The **Create an AWS Secret** form displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (605).png" alt=""><figcaption><p><strong>Create an AWS Secret</strong> form</p></figcaption></figure></div>
4. Fill in the fields as described below:

<table data-header-hidden><thead><tr><th width="229.11102294921875">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for this secret.</td></tr><tr><td><strong>Secret value type (Json or plain text)</strong></td><td><p>Specify the secret type:<br></p><ul><li><strong>JSON Key/Value pairs</strong>: Store your secret as structured key-value pairs (e.g., credentials or connection settings).</li><li><strong>Plain text</strong>: Store your secret as a single unstructured plaintext string.</li></ul></td></tr><tr><td><strong>JSON (key value pair)</strong> <br><em>(if <strong>JSON Key/Value pairs</strong> selected)</em></td><td>Enter your secret data as JSON key/value pairs. <br><strong>Note</strong>: all values must be strings. This means you must enclose numbers and Booleans in double quotes. For example, use <code>"5432"</code> instead of <code>5432</code>, and <code>"true"</code> instead of <code>true</code>.</td></tr><tr><td><em><strong>Value</strong></em><br><em>(shown if <strong>Plain text</strong> selected)</em></td><td>Enter your secret as a plaintext string, e.g., <code>mysecretvalue123</code>.</td></tr></tbody></table>

5. Click **Create** to create the secret in AWS Secrets Manager. The secret will be created directly in AWS using the credentials associated with your DuploCloud environment.&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot (606).png" alt=""><figcaption><p><strong>AWS Secrets</strong> tab in the DuploCloud Platform</p></figcaption></figure>

{% hint style="info" %}
In environments with **tag-based resource management**, DuploCloud may automatically tag secrets with Tenant or application metadata. Access to secrets may also be restricted based on these tags.
{% endhint %}

## Managing AWS Secrets

You can view, edit, or deletes directly from the DuploCloud Portal.

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **App Integration**.
2. Select the **AWS Secrets** tab
3.  Click the menu icon (<img src="../../../.gitbook/assets/menu icon (2).avif" alt="" data-size="line">) in the row of the secret you want to manage.\


    <figure><img src="../../../.gitbook/assets/Screenshot (607).png" alt=""><figcaption><p><strong>AWS Secrets</strong> tab with the secret menu options highlighted</p></figcaption></figure>
4. Select one of the following options:

<table data-header-hidden><thead><tr><th width="192.6666259765625">Action</th><th>Description</th></tr></thead><tbody><tr><td><strong>View Secret</strong></td><td>View the secret details and metadata.</td></tr><tr><td><strong>JSON</strong></td><td>View the secret’s value formatted as JSON (for JSON secrets).</td></tr><tr><td><strong>Edit Secret</strong></td><td>Modify the secret’s value or metadata.</td></tr><tr><td><strong>Console</strong></td><td>Open the AWS Secrets Manager console directly for this secret.</td></tr><tr><td><strong>Delete</strong></td><td>Remove the secret from DuploCloud and AWS.</td></tr></tbody></table>

## Additional Resources

* [AWS Secrets Manager Documentation](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) – Learn more about securely storing, retrieving, and managing secrets using AWS Secrets Manager.
* [AWS IAM for Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/auth-and-access.html) – Understand how to manage access and permissions for your secrets using AWS Identity and Access Management (IAM).
* [Kubernetes SecretProviderClass in DuploCloud](../../kubernetes-overview/configs-and-secrets/adding-secretproviderclass-custom-resource.md) – Learn how to mount AWS Secrets into Kubernetes Pods using SecretProviderClass.
