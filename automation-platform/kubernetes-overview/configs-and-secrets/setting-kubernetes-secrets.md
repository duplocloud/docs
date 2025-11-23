---
description: >-
  Set and manage Kubernetes Secrets in the DuploCloud Portal, including
  troubleshooting format issues.
---

# Setting Kubernetes Secrets

Kubernetes `Secrets` allow you to securely store and manage sensitive information—such as passwords, tokens, and keys—separately from your application code. This page covers how to define and manage those secrets in DuploCloud.

To securely manage Kubernetes secrets, follow these best practices:

* **Utilize Centralized Secret Management Tools** to streamline storage, versioning, and access control.
* **Implement Access Controls** to ensure only authorized users and workloads can access or modify secrets.
* **Regularly Rotate Secrets** to limit exposure if a secret is compromised.
* **Audit Access Logs** to monitor for unauthorized access or anomalies.

By using these strategies alongside DuploCloud's interface for Kubernetes secrets, you can enforce secure and maintainable secret management across your environments.

## Creating a Kubernetes Secret&#x20;

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Secrets**.
2.  Click **Add**. The **Add Kubernetes Secret** pane displays.<br>

    <div align="left"><img src="../../../.gitbook/assets/Screen Shot 2022-03-21 at 12.50.14 PM.png" alt="Add Kubernetes Secret pane" width="563"></div>
3. Complete the fields:

<table data-header-hidden><thead><tr><th width="163.33331298828125"></th><th></th></tr></thead><tbody><tr><td><strong>Secret Name</strong></td><td>A unique name for the secret (e.g., <code>my-secret-files</code>).</td></tr><tr><td><strong>Secret Type</strong></td><td>Enter the Kubernetes secret type (e.g., <code>Opaque</code>, <code>kubernetes.io/dockerconfigjson</code>, etc). Choose <code>Opaque</code> for generic key/value pairs.</td></tr><tr><td><strong>Secret Details</strong></td><td>Enter the key/value pairs that make up the secret. Use the format <code>key: value</code> per line, where the key is the filename and the value is its contents.</td></tr></tbody></table>

3. Click **Add** to create the secret.

To use this Secret in your application, [mount it as a volume in a container](mounting-config-as-files.md#mounting-a-kubernetes-secret-as-a-volume).

## Creating a multi-line Kubernetes Secret

1.  Follow the steps in [creating a Kubernetes Secret](setting-kubernetes-secrets.md#creating-a-kubernetes-secret), defining a Key value using the `PRIVATE_KEY_FILENAME`  in the **Secret Details** field, as shown below. <br>

    <div align="left"><img src="../../../.gitbook/assets/Screen Shot 2022-08-10 at 4.25.05 PM.png" alt="" width="563"></div>
2. Click **Add** to create the multi-line secret.

To use this Secret in your application, [mount it as a volume in a container](mounting-config-as-files.md#mounting-a-kubernetes-secret-as-a-volume).

<figure><img src="../../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.14-14_46_22.png" alt=""><figcaption><p>The <strong>Kubernetes Secrets</strong> page in the DuploCloud Portal</p></figcaption></figure>

## Troubleshooting Secret Format Issues

When entering a Kubernetes secret with a private key in Duplo, ensure the data is formatted as key/value pairs with all keys and values as strings. If you encounter format errors, it's likely due to non-string values or incorrect multiline string formatting. Use the `|` character to indicate multiline strings and manually split a single-line private key into multiple lines for compatibility. Matching the format of an existing, working secret can also aid in resolving these issues.
