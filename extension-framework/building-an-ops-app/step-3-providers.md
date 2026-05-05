# Step 3: Connect Providers

A provider is any IT system your application will orchestrate. You register providers, supply credentials, and define scopes that control what the agent can access. Providers are what give your Ops application reach — without them, the agent has instructions but no systems to act on.

## What Is a Provider

A provider represents an external system the platform needs to access. Providers span every category of IT system an operations team might work with:

- **Cloud accounts**: AWS, Azure, GCP
- **Kubernetes clusters**: EKS, AKS, GKE, or any conformant cluster
- **Source control**: GitHub, GitLab, Bitbucket
- **CRM and sales tools**: Salesforce, Apollo, Outreach, Lemlist
- **Observability platforms**: Datadog, New Relic
- **Incident management**: PagerDuty, ServiceNow
- **Compliance and GRC tools**: Vanta, Drata
- **Any other system** accessible via MCP servers

If a system exposes an API or CLI, it can be registered as a provider. The framework does not constrain which systems you can connect — the MCP server model means coverage extends to anything with an accessible interface.

## Registering a Provider

To register a provider, supply its type, connection details, and credentials. Credentials are stored securely in the platform and are never exposed to users or surfaced in agent conversations. The agent receives credentials as structured data at ticket dispatch time, translates them into the file formats the underlying CLIs and SDKs expect (kubeconfig, AWS credential files, application default credentials, etc.), and cleans them up when the session ends.

When a user creates a ticket or resource, they select a scope — not a credential. They never see or handle the underlying authentication material.

## Configuring Scopes

A scope combines three things: a provider, a credential, and granular access controls. Access controls can restrict the agent to specific regions, resource types, namespaces, or custom resource maps — whatever level of precision your security requirements demand.

Scopes are reusable. The same scope can be attached to multiple workspaces, giving different teams access to the same underlying system without duplicating configuration. A "production AWS us-east-1" scope can be assigned to a Platform Engineering workspace with full write access and also to an L1 SRE workspace with read-only access — same provider and credential, different permission boundaries.

When a user selects a scope at ticket creation time, that selection determines which IT systems the agent can operate on for the duration of the ticket. The agent cannot exceed the scope's boundaries regardless of what it reasons.

{% hint style="info" %}
For provider-specific setup guides — including credential formats, supported regions, and MCP server configuration — see [Integrating Providers](../../getting-started/integrating-providers/).
{% endhint %}
