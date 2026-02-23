# Providers

Providers store credentials for connecting to cloud accounts, Kubernetes namespaces, incident tools, and other services. After adding Providers, you create Scopes that define what resources can be accessed. Permissions are then granted by assigning these Scopes to Engineers when creating or editing them.

## Adding Providers and Defining Access Scopes

1. Navigate to to **Providers** and select the tab for the Provider type you are trying to add, e.g., **Cloud**, **Kubernetes**, etc. The available Provider types are listed in the table below. To add a Provider type that is not listed, contact your DuploCloud Support team on Slack or via email at support@duplocloud.net.

<figure><img src="../../.gitbook/assets/unknown (2).png" alt=""><figcaption></figcaption></figure>

| Cloud Providers     | AWS, GCP, Azure                                                           |
| ------------------- | ------------------------------------------------------------------------- |
| Kubernetes          | EKS, AKS, GKE, RHOS                                                       |
| Observability       | OpenTelemetry (Otel), Datadog, New Relic, Sentry                          |
| Incident Management | Grafana Alert Manager, Datadog, New Relic, Sentry, PagerDuty, Incident.io |
| Git Repositories    | GitHub, GitLab, Bitbucket                                                 |

2. Click **Add**. The **Edit Provider** screen displays, showing the relevant inputs required for connecting to that Provider type.&#x20;
3. Complete the required fields.&#x20;

<figure><img src="../../.gitbook/assets/Image" alt=""><figcaption></figcaption></figure>

4. Click **Update** to finish granting access. This will return you to the Provider’s screen.&#x20;

<figure><img src="../../.gitbook/assets/unknown (3).png" alt=""><figcaption></figcaption></figure>

5. Select the **Credentials** tab, and click **Add**. The **Edit Credential** pane displays.
6. Enter the credential specification, and click **Update**. This will return you to the Provider’s screen.&#x20;

<figure><img src="../../.gitbook/assets/unknown (4).png" alt=""><figcaption></figcaption></figure>

7. Click **Scope** and then **Add Scope**. Give the Scope a suitable name and description, select one of the credentials added and (optionally) select an MCP Server. Enter the resource map in **Key: Values** format.
8. Click **Create**.

<figure><img src="../../.gitbook/assets/unknown (5).png" alt=""><figcaption></figcaption></figure>

Now, you can move on to creating access for MCP Servers for your Engineers.&#x20;
