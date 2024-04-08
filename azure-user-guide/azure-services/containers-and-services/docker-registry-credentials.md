---
description: Set Docker registry credentials
---

# Docker Registry Credentials

## Set Docker Registry Credentials and Kubernetes Secrets

1. In the DuploCloud Portal, navigate to  **DevOps** -> **Containers** -> **AKS/Native**. Docker registry credentials are passed to the Kubernetes cluster as `kubernetes.io/dockerconfigjson`.
2. Click **Docker Credentials**. The **Set Docker registry Creds** pane displays.
3. Supply the credentials and click **Submit**.
4. Enable the Docker Shell Service by clicking **Enable Docker Shell**.

## Add multiple Docker Registry Credentials

You can pull images from multiple Docker registries by adding multiple Docker Registry Credentials.

1. In the DuploCloud Portal, click **Administrator**-> **Plan**. The **Plans** page displays. &#x20;
2. Select the Plan in the **Name** column.
3. Click the **Config** tab.
4. Click **Add**. The **Add Config** pane displays.

<figure><img src="../../../.gitbook/assets/aws_add_config (2).png" alt=""><figcaption><p><strong>Add Config</strong> pane</p></figcaption></figure>

## Access Kubernetes ConfigMaps using file and Environment Variables (EVs)

See the [Prerequisite section](passing-config-and-secrets.md) for details.
