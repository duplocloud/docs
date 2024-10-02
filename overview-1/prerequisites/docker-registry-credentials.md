# \[Optional] Docker Registry Credentials



{% hint style="info" %}
This step is needed only if you are using an external non GCR registry
{% endhint %}

## Set Docker Registry Credentials&#x20;

1. In the DuploCloud Portal, navigate to **Docker** -> **Services**. Docker registry credentials are passed to the Kubernetes cluster as `kubernetes.io/dockerconfigjson`.
2. Click the **Docker** item list in the upper right and select **Docker Credentials**. The **Set Docker registry Creds** pane displays.
3. Supply the credentials and click **Submit**.
4. Enable the Docker Shell Service by clicking **Enable Docker Shell**.

## Add multiple Docker Registry Credentials

You can pull images from multiple Docker registries by adding multiple Docker Registry Credentials.

1. In the DuploCloud Portal, click **Administrator** -> **Plan**. The **Plans** page displays. &#x20;
2. Select the Plan in the **Name** column.
3. Click the **Config** tab.
4. Click **Add**. The **Add Config** pane displays.

<div align="left">

<figure><img src="../../.gitbook/assets/aws_add_config.png" alt=""><figcaption><p><strong>Add Config</strong> pane</p></figcaption></figure>

</div>
