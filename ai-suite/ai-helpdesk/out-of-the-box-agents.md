---
description: An overview of DuploCloud's pre-built AI Agents
---

# Out of the Box Agents

DuploCloud AI Suite includes several pre-built, production-ready agents that handle common DevOps and infrastructure management tasks. These agents integrate seamlessly with your existing DuploCloud infrastructure and can be deployed immediately to automate routine operations and troubleshooting workflows.

Agents work within DuploCloud's secure tenant architecture, inheriting user permissions and maintaining compliance with your organization's security policies. Agents can be accessed through the HelpDesk interface, where you can create tickets and collaborate with AI agents to resolve issues or perform tasks.

## Out-of-the-Box Agents

### Kubernetes Agent

The Kubernetes Agent is an expert DevOps engineer specialized in Kubernetes cluster management, maintenance, and troubleshooting. This agent serves as your dedicated Kubernetes specialist, capable of handling everything from routine cluster health checks to complex resource deployments.

<details>

<summary>View Kubernetes Agent details</summary>

#### Core Capabilities

* **Cluster Health Monitoring**: Assess overall cluster health and identify potential issues
* **Resource Management**: Create, update, and manage Kubernetes resources (pods, services, deployments, etc.)
* **Troubleshooting**: Diagnose and resolve pod failures, networking issues, and resource constraints
* **Log Analysis**: Retrieve and analyze logs from specific pods or services
* **Resource Inspection**: Detailed examination of Kubernetes objects and their configurations

#### Key Features

* **Permission Inheritance**: Operates with the requesting user's Kubernetes permissions - no additional access required
* **kubectl Integration**: Executes kubectl commands securely within your cluster environment
* **Multi-Level Support**: Handles both specific detailed requests (like "get logs for pod xyz") and high-level queries (like "assess cluster health")
* **Real-time Troubleshooting**: Interactive problem-solving with immediate command execution

#### Use Cases

* Investigating pod startup failures or crashes
* Analyzing resource utilization and capacity planning
* Deploying new applications or updating existing ones
* Troubleshooting networking and service connectivity issues
* Performing routine maintenance tasks and health checks

#### Security Model

* No standalone permissions - inherits user's existing kubectl access
* All actions are performed within DuploCloud's tenant isolation
* Command execution is logged and auditable

</details>

### Observability Agent

The Observability Agent provides intelligent monitoring and troubleshooting capabilities through integration with your observability stack. It is currently optimized for OpenTelemetry-based environments using Grafana and helps teams quickly identify and resolve application performance issues.

<details>

<summary>View Observability Agent details</summary>

#### Core Capabilities

* **Log Retrieval and Analysis**: Fetch and summarize logs from Grafana with intelligent pattern recognition
* **Metrics Analysis**: Query and interpret application and infrastructure metrics
* **Contextual Filtering**: Automatically scope queries to the user's current namespace
* **Pattern Detection**: Identify anomalies and trends in log data
* **Time-based Analysis**: Analyze data across specific time windows

#### Current Implementation

* **Backend**: OpenTelemetry with Grafana integration
* **Data Types**: Logs and metrics (traces, spans, and profiles coming in future versions)
* **Scope**: Namespace-aware operations

#### Key Features

* **Namespace Awareness**: Automatically understands user's operational context
* **Natural Language Queries**: Ask questions like "show me errors in the payment service from the last hour"
* **Pattern Recognition**: Automatically identifies common error patterns and anomalies
* **Dashboard Navigation**: Guides users to relevant Grafana dashboards and visualizations

#### Use Cases

* Investigating application errors and performance degradation
* Analyzing traffic patterns and resource utilization
* Troubleshooting microservice communication issues
* Monitoring application health across environments
* Root cause analysis for incidents

#### Roadmap

Future versions will include support for:

* Distributed tracing analysis
* Span-level troubleshooting
* Performance profiling insights
* Integration with additional observability platforms (e.g., Datadog, New Relic, Kibana)

</details>

### CI/CD Agent

The CI/CD Agent automates pipeline troubleshooting and failure resolution across your continuous integration and deployment workflows. Available for both Jenkins and GitHub Actions, this agent proactively engages when pipeline failures occur and provides intelligent assistance for resolution.

<details>

<summary>View CI/CD Agent details</summary>

#### Supported Platforms

* **Jenkins**: Full integration with Jenkins pipelines and build processes
* **GitHub Actions**: Native GitHub Actions workflow support

#### Core Capabilities

* **Automatic Failure Detection**: Triggered automatically when pipeline failures occur
* **Intelligent Troubleshooting**: Analyzes failure logs and provides resolution recommendations
* **Deep Investigation**: Can retrieve additional logs, files, and context when needed
* **Pipeline Context**: Full understanding of build history, dependencies, and configurations

#### Integration Workflow

1. **Failure Detection**: Try-catch blocks in your pipelines automatically detect failures
2. **Ticket Creation**: DuploCloud CLI (duploctl) creates HelpDesk tickets with full context
3. **Agent Assignment**: Tickets are automatically assigned to the CI/CD agent
4. **Resolution Process**: Agent analyzes logs and works with users to resolve issues

#### Key Features

* **Automatic Ticket Creation**: No manual intervention required for failure detection
* **Rich Context**: Receives pipeline output, URLs, execution IDs, and failure details
* **Cross-Platform Access**: Can access version control, retrieve files, and examine build artifacts
* **Pipeline History**: Understands build trends and recurring failure patterns
* **Seamless Integration**: Direct links from Jenkins/GitHub Actions to HelpDesk tickets

#### Use Cases

* Debugging build failures and compilation errors
* Resolving deployment issues and rollback scenarios
* Optimizing pipeline performance and reliability

</details>

### Architecture Diagram Agent

The Architecture Diagram Agent leverages DuploCloud's cartography system to generate intelligent infrastructure and application architecture diagrams. Built on Neo4j graph database technology, this agent provides visual representations of complex system relationships and dependencies.

<details>

<summary>View Architecture Diagram Agent details</summary>

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

</details>

### PrivateGPT Agent

The PrivateGPT Agent provides a secure, enterprise-grade ChatGPT-like experience for organizations concerned about data privacy and security. This agent ensures that sensitive organizational data never leaves your AWS environment while providing powerful AI assistance.

<details>

<summary>View PrivateGPT Agent details</summary>

#### Security Architecture

* **Data Locality**: All processing occurs within your AWS environment
* **AWS Bedrock Backend**: Leverages AWS Bedrock for LLM capabilities
* **Enhanced Privacy**: Stronger guarantees that input data won't be used for model training
* **DuploCloud Interface**: Access through familiar HelpDesk interface

#### Core Capabilities

* **General AI Assistance**: Natural language processing for various business needs
* **Document Analysis**: Process and analyze internal documents securely

#### Key Features

* **Zero External Data Exposure**: All interactions remain within your cloud environment
* **Familiar Interface**: ChatGPT-like experience through DuploCloud HelpDesk
* **Enterprise Controls**: Full audit trail and access controls
* **Compliance Ready**: Meets strict data residency and privacy requirements

#### Use Cases

* Analyzing sensitive business documents
* Internal knowledge base queries
* Compliance and regulatory document review

#### Benefits Over Public AI Services

* **Data Sovereignty**: Complete control over where your data is processed
* **Compliance Alignment**: Meets enterprise security and regulatory requirements
* **Audit Trail**: Full logging and monitoring of AI interactions

</details>

### Database Explorer Agent

The Database Explorer Agent provides secure, controlled access to database operations through pre-defined query templates. This agent enables non-technical teams to access database information safely without SQL knowledge or direct database access.

<details>

<summary>View Database Explorer Agent details</summary>

#### Core Architecture

* **Template-Based Queries**: Uses pre-defined "fuzzy" SQL query templates
* **Multi-Database Support**: Works with MySQL, PostgreSQL, and other relational databases
* **Natural Language Interface**: Users interact using plain language requests
* **Parameter Substitution**: Intelligently fills in query parameters based on user input

#### Security Model

* **Controlled Access**: Only pre-approved query patterns can be executed
* **No Raw SQL**: Users cannot execute arbitrary database commands
* **Template Validation**: All queries must match predefined templates
* **Audit Logging**: Complete tracking of all database interactions

**User Interaction**

* **User Request**: "Find the customer with phone number (555) 123-4567"
* **Agent Processing**: Extracts phone number, maps to customer lookup template
* **Query Execution**: Substitutes parameter and executes safe query
* **Response**: Returns customer information in user-friendly format

#### Key Features

* **Template Library**: Maintain a collection of approved query patterns
* **Parameter Validation**: Automatic validation of input parameters
* **Result Formatting**: Present database results in user-friendly formats

#### Use Cases

* **Customer Support**: Quick customer information lookup
* **Data Analysis**: Self-service access to business intelligence data
* **Report Generation**: Automated generation of standard reports
* **Operational Queries**: Access to operational data without technical expertise

#### Benefits

* **Rapid Development**: Enable data access without building custom UIs
* **Security**: Controlled access prevents unauthorized operations
* **User Empowerment**: Non-technical teams gain self-service capabilities
* **Reduced Development Overhead**: No need to build custom data access interfaces

</details>

## Support and Customization

While these out-of-the-box agents cover many common use cases, DuploCloud's AI Studio platform enables you to build custom agents tailored to your specific workflows and tools. For assistance with agent customization or integration with additional tools, contact the DuploCloud team.
