# Supporting Components

### Cartography

DuploCloud Cartography is a Dockerized build of Cartography extended with custom DuploCloud intelligence and Neo4j models that unifies DuploCloud, Kubernetes, AWS, GitHub, and external systems into a single, queryable graph. It injects a Duplo ingestion stage at runtime (via sitecustomize) to ingest Tenants, Plans, Infrastructures, Hosts, Pods, Agents, and container versions, standardizing on IN\_TENANT relationships for clean scoping and authorization. The project supports an optional dependencies manifest (local file or Kubernetes ConfigMap) to link workloads to Kubernetes objects, AWS resources (e.g., S3, RDS), and external services, while helper scripts and JIT credential support make it straightforward to run against Neo4j for local development or production.

{% content-ref url="view-cartography-details.md" %}
[view-cartography-details.md](view-cartography-details.md)
{% endcontent-ref %}

### GenAI-ToolBox

### Presidio

The **Duplo Presidio Service** is a wrapper built on top of Microsoft Presidio that enhances its ability to detect and protect sensitive data by allowing **custom recognizers and anonymizers**.\
This ensures secrets, tokens, and credentials are automatically identified and protected before data leaves your Duplo-managed Kubernetes cluster.

{% content-ref url="view-presidio-details.md" %}
[view-presidio-details.md](view-presidio-details.md)
{% endcontent-ref %}
