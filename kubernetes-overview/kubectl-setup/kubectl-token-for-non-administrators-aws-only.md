---
description: Access kubectl without administrator privileges
---

# Kubectl Token for non-administrators

If you don't have administrator privileges, use this procedure to access `kubeconfig` using the `kubectl` token. `kubeconfig` is a YAML file that stores cluster authentication information for kubectl. It contains a list of contexts to which kubectl refers when running commands. By default, `kubeconfig` is saved in the `$HOME/` directory in the Linux operating system.

{% hint style="warning" %}
Before beginning, refer to this article for more information about[`kubeconfig`](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/).
{% endhint %}

## Updating the AWS Profile (AWS Only)&#x20;

Add the following code to your AWS profile:

```yaml
[profile NAME] # Supply your AWS profile name
region=us-east-1
credential_process=duplo-aws-credential-process --tenant YOUR_TENANT --host --interactive
```

## Downloading the `kubectl` token

{% hint style="info" %}
The token that you download is for the selected Tenant only. It is intended for use with a non-human DuploCloud service account.
{% endhint %}

1. In the DuploCloud Portal, navigate to **Kubernetes** -> **Services**. The **Services** page displays.
2. Select the Service name from the **Name** column.
3.  From the **KubeCtl** item list, select **KubeCtl Token**. The **KubeCtl Token** window displays.\


    <figure><img src="../../.gitbook/assets/Screenshot (350).png" alt=""><figcaption><p><strong>Token</strong> window with <code>kubectl</code> commands for creating token</p></figcaption></figure>
4. Click **Copy** to copy the `kubectl` commands in the **Token** window to your clipboard.
5. From the **KubeCtl** item list, select **KubeCtl Shell** to launch the shell instance. Paste the copied commands into the shell and run them.
