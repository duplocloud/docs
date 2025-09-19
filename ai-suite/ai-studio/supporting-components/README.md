# Supporting Components

### Cartography

Duplo Cartography is a Dockerized build of Cartography extended with custom Duplo intelligence and Neo4j models that unifies DuploCloud, Kubernetes, AWS, GitHub, and external systems into a single, queryable graph. It injects a Duplo ingestion stage at runtime (via sitecustomize) to ingest tenants, plans, infra, hosts, pods, agents, and container versions, standardizing on IN\_TENANT relationships for clean scoping and authorization. The project supports an optional dependencies manifest (local file or Kubernetes ConfigMap) to link workloads to Kubernetes objects, AWS resources (e.g., S3, RDS), and external services, while helper scripts and JIT credential support make it straightforward to run against Neo4j for local development or production.



{% content-ref url="view-cartography-details.md" %}
[view-cartography-details.md](view-cartography-details.md)
{% endcontent-ref %}



### GenAI-ToolBox

### Presidio

Presidio Service is a wrapper built on top of Microsoft’s open-source Presidio framework, designed to detect and protect sensitive data such as PII, credentials, tokens, and secrets. While Presidio provides strong built-in capabilities, the Duplo wrapper extends it by supporting custom recognizers, enabling organizations to define their own detection rules for environment-specific secrets (e.g., API keys, database passwords, private keys). Running as a Kubernetes microservice within Duplo-managed clusters, it ensures sensitive data is anonymized or sanitized before leaving the environment—strengthening compliance, privacy, and security across applications and integrations with external services like LLMs.



{% content-ref url="view-presidio-details.md" %}
[view-presidio-details.md](view-presidio-details.md)
{% endcontent-ref %}
