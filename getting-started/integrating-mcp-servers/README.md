# DuploCloud MCP Integration

DuploCloud's AI platform supports the **Model Context Protocol (MCP)**, an open standard that enables AI agents to connect directly to external tools and services. Through the DuploCloud AI Studio, administrators can register any MCP-compatible server as a provider integration, giving the AI agent live, contextual access to third-party observability, incident management, source control, and other platforms.

Once an MCP server is registered, it is attached to a provider scope alongside credentials and resource configuration. At session start, the DuploCloud agent automatically constructs the appropriate MCP configuration and injects it into the agent's environment — no manual setup required for end users.

This integration is designed to extend the agent's capabilities beyond infrastructure management. With connected MCP servers, the agent can query error logs, inspect monitors, triage incidents, browse repositories, and take action across platforms — all through natural language, from within a single interface.

DuploCloud supports **API key and token-based authentication** for MCP servers via HTTP headers configured in the provider scope's Resource Map. Note that **OAuth-based authentication is not currently supported** — MCP servers requiring an interactive OAuth flow cannot be connected through the DuploCloud platform at this time.

Providers already modelled in the platform include observability tools like Datadog, New Relic, and Sentry, incident management platforms like PagerDuty and Incident.io, and source control providers like GitHub and GitLab — making DuploCloud's AI agent a central hub for cross-platform infrastructure intelligence.