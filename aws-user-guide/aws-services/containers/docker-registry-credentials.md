---
description: Set Docker registry credentials
---

# Docker Registry credentials

## Setting Docker Registry Credentials

To authenticate with private Docker registries, DuploCloud utilizes Kubernetes secrets of type `kubernetes.io/dockerconfigjson`. This process involves specifying the registry URL and credentials in a `.dockerconfigjson` format, which can be done in two ways:

1. **Base64 Encoded Username and Password:** Encode the username and password in Base64 and include it in the `.dockerconfigjson` secret.
2. **Raw Username and Password:** Directly use the `username` and `password` in the secret without Base64 encoding. This method is supported and simplifies the process by not requiring the `auth` field to be Base64 encoded.

1. In the DuploCloud Portal, navigate to **Docker** -> **Services**. 
2. From the **Docker** list box, select **Docker Credentials**. The **Set Docker registry Creds** pane displays.
3. Supply the credentials in the required format and click **Submit**.
4. Enable the Docker Shell Service by selecting **Enable Docker Shell** from the **Docker** list box.

If you encounter errors such as a pull access denied or a failure to resolve reference due to authorization issues, ensure the secret is correctly configured and referenced in your service configuration. For non-default repositories, explicitly mention the `imagePullSecrets` with the name of the docker authentication secret to resolve image pulling issues:

```yaml
imagePullSecrets:
  - name: docker-qa-auth
```

## Adding multiple Docker Registry Credentials

You can pull images from multiple Docker registries by adding multiple Docker Registry Credentials.

1. In the DuploCloud Portal, click **Administrator**-> **Plan**. The **Plans** page displays. 
2. Select the Plan in the **Name** column.
3. Click the **Config** tab.
4. Click **Add**. The **Add Config** pane displays.

### Passing Docker Credentials using Environment Variables

Docker Credentials can also be passed using the Environment Variables config field in the **Add Service Basic Options** page. This method is particularly useful for dynamically supplying credentials without hardcoding them into your service configurations. Refer to the [Kubernetes Configs and Secrets](../../../kubernetes-user-guide/configs-and-secrets/) section for more details on how to use environment variables for passing secrets.

Ensure all required secrets, like `imagePullSecrets` for Docker authentication, are correctly added and referenced in the service configuration to avoid invalid config issues with a service. Reviewing the service configuration for any missing or incorrectly specified parameters is crucial for smooth operation.