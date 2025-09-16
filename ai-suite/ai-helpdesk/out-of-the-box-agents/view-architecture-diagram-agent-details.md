# View Architecture Diagram Agent details

#### Core Technology

* **Backend**: Neo4j graph database populated by DuploCloud Cartography
* **Real-time Updates**: Continuously synchronized with your cloud environment
* **Multi-layer Mapping**: Covers AWS resources, Kubernetes objects, and application dependencies
* **Visualization**: Mermaid.js diagram generation

#### Key Features

* **Developer-Centric Views**: Generate diagrams focused on specific microservices or applications
* **Multi-Level Detail**: From high-level architecture overviews to detailed resource dependencies
* **Interactive Exploration**: Ask questions like "show me everything connected to the payment service"
* **Real-time Accuracy**: Diagrams reflect current state of your infrastructure
* **Contextual Filtering**: Scope diagrams to specific tenants, namespaces, or applications

#### Use Cases

* **New Developer Onboarding**: Help developers understand system architecture for unfamiliar services
* **Impact Analysis**: Visualize dependencies before making changes
* **Troubleshooting**: Understand data flow and potential failure points
* **Documentation**: Generate up-to-date architecture documentation
* **Compliance Auditing**: Visualize data flows for security and compliance reviews

#### Custom Dependency Definition

Organizations can optionally define custom application dependencies:

* **Granular Control**: Define dependencies per microservice
* **Multi-type Support**: AWS resources, Kubernetes services, and external APIs

\
**Architecture Diagram Agent — Role Boundaries and Scope**

* **Tenancy boundary**:
  * Every resource, relationship, metric, and event is namespaced by `tenantId`.
  * All reads/writes require a `tenantId`; data from other tenants is never returned or mutated.
  * Cross-tenant access is denied; background jobs and graph updates run within the same `tenantId` scope.
* **User role (least privilege)**:
  * **Visibility**: Only resources and relationships within their own `tenantId`.
  * **Actions**: Read and interact within tenant scope; cannot access or reference other tenants.
  * **UI**: Graph, search, filters, impact/stats panels, and websockets show only tenant-scoped data.
* **Admin role (most privilege)**:
  * **Visibility**: Intended for administration across tenants.
  * **Actions**: Manage resources, relationships, and system-wide operations.
  * **UI**: Can view and operate beyond a single tenant unless least-privilege applies (see below).
* **Least-privilege override (effective role)**:
  * When a principal has multiple roles, the least-privileged role determines access.
  * Example: If a principal has both admin and user roles, the effective scope is the user role:
    * Visibility and actions are restricted to the principal’s `tenantId`.
    * Cross-tenant views and operations are not permitted.
* **What each role sees**:
  * **User**: Only their tenant’s nodes, edges, metrics, and events; tenant-filtered diagrams and panels.
  * **Admin**: System-wide view and management; however, if also assigned the user role, the session is constrained to the user’s single-tenant scope.
* **Enforcement points (high level)**:
  * API routes validate and require `tenantId`.
  * Graph/database queries filter by `tenantId`.
  * Websocket channels are namespaced by `tenantId`.
  * Diagram generation and analysis features apply `tenantId` filtering end-to-end.

In short: data is strictly segmented by `tenantId`; users operate only within their tenant; admins can operate broadly, but any concurrent user assignment forces least-privilege behavior, restricting access to the user’s tenant.
