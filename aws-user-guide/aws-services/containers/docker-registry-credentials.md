---
description: Set Docker registry credentials
---

# Docker Registry credentials

## Setting Docker Registry Credentials&#x20;

1. In the DuploCloud Portal, navigate to **Docker** -> **Services**. Docker registry credentials are passed to the Kubernetes cluster as `kubernetes.io/dockerconfigjson`.
2. From the **Docker** list box, select **Docker Credentials**. The **Set Docker registry Creds** pane displays.
3. Supply the credentials and click **Submit**.
4. Enable the Docker Shell Service by selecting **Enable Docker Shell** from the **Docker** list box.

## Adding multiple Docker Registry Credentials

You can pull images from multiple Docker registries by adding multiple Docker Registry Credentials.

1. In the DuploCloud Portal, click **Administrator**-> **Plan**. The **Plans** page displays. &#x20;
2. Select the Plan in the **Name** column.
3. Click the **Config** tab.
4. Click **Add**. The **Add Config** pane displays.

<div align="left">

<figure><img src="../../../.gitbook/assets/aws_add_config (2).png" alt=""><figcaption><p><strong>Add Config</strong> pane</p></figcaption></figure>

</div>

### Passing Docker Credentials using Environment Variables

You can pass Docker Credentials using the Environment Variables config field in the **Add Service Basic Options** page. See the [Kubernetes Configs and Secrets](../../../kubernetes-user-guide/configs-and-secrets/) section for details.
