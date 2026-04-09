---
description: Integrations with your IT systems
---

# Providers

Providers represent the access you provide to your IT systems - including cloud accounts, Kubernetes namespaces, Git repositories, incident management tools, and other services. After adding Providers, you can supply credentials and create Scopes that define what resources can be accessed. These permissions are then inherited by Workspaces when they are granted access to the right scopes.&#x20;

## Adding Providers and Defining Scopes

1. Navigate to **Providers** and select the tab for the Provider type you are trying to add, e.g., **Cloud**, **Kubernetes**, etc. The available Provider types are listed in the table below. To add a Provider type that is not listed, contact your DuploCloud Support team on Slack or via email at support@duplocloud.com.

<figure><img src="../../.gitbook/assets/Provider 1.png" alt=""><figcaption></figcaption></figure>

| Cloud Providers     | AWS, GCP, Azure                                                           |
| ------------------- | ------------------------------------------------------------------------- |
| Kubernetes          | EKS, AKS, GKE, RHOS                                                       |
| Observability       | OpenTelemetry (Otel), Datadog, New Relic, Sentry                          |
| Incident Management | Grafana Alert Manager, Datadog, New Relic, Sentry, PagerDuty, Incident.io |
| Source Control      | GitHub, GitLab, Bitbucket                                                 |
| GRC tools           | Vanta, Drata                                                              |

2. Click **Add**. The **Add Provider** screen displays, showing the relevant inputs required for connecting to that Provider type.&#x20;
3. Complete the required fields.&#x20;

<figure><img src="../../.gitbook/assets/Provider 2.png" alt=""><figcaption></figcaption></figure>

4. Click **Update** to finish granting access. This will return you to the Provider’s screen.&#x20;

<figure><img src="../../.gitbook/assets/Provider 3.png" alt=""><figcaption></figcaption></figure>

5. Select the **Credentials** tab and click **Add**. The **Add Credential** pane displays.
6. Enter the credential specification, and click **Update**. This will return you to the Provider’s screen.&#x20;

<figure><img src="../../.gitbook/assets/Provider 4.png" alt=""><figcaption></figcaption></figure>

7. Click **Scope** and then **Add Scope**. Give the Scope a suitable name and description, select one of the added credentials and (optionally) select an MCP Server. Enter the resource map in **Key:Value** format.
8. Click **Create**.

<figure><img src="../../.gitbook/assets/Provider 5.png" alt=""><figcaption></figcaption></figure>



Now, we can move on to creating access to MCP Servers.&#x20;
