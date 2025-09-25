# AI Studio

Agents in DuploCloud AI Studio are specialized AI components designed to perform specific DevOps and infrastructure management functions. Each Agent serves as a dedicated expert in areas such as Kubernetes troubleshooting, observability analysis, CI/CD operations, or security monitoring. Built on foundation models and enhanced with the knowledge graph the DuploCloud DevOps Automation Platform provides.&#x20;

## Agent Definitions

Agent definitions form the blueprint for creating AI Agents within DuploCloud AI Studio. These definitions specify the Agent's capabilities, LLM, and knowledge sources. Each definition includes parameters such as the base model to use, required tools, permission scopes, and response formats. Agent definitions are version-controlled, allowing for systematic improvement and rollback capabilities. This declarative approach to Agent creation ensures consistency, reusability, and transparent governance of AI capabilities across your organization.

### Prebuilt Agents

Prebuilt Agents are ready-to-use solutions developed outside of AI Studio that conform to DuploCloud's agent standards and interfaces. These Agents are packaged as Docker images with pre-configured APIs that seamlessly integrate with the AI HelpDesk. Prebuilt agents offer immediate value for common DevOps scenarios without requiring custom development. They're ideal for organizations seeking to rapidly implement AI assistance for standardized workflows or those with existing Agent implementations they wish to incorporate into the DuploCloud ecosystem.&#x20;

### Dynamic Agents

Dynamic Agents are built using DuploCloud's LangChain-based framework, allowing for flexible, composable Agentic AI solutions tailored to specific operational needs. These Agents are constructed at build time by combining a base Agent configuration with selected Tools from the AI Studio repository. The LangChain architecture enables dynamic Agents to reason through complex problems, execute appropriate Tools based on context, and maintain coherent conversations with users. This approach facilitates rapid prototyping and iteration, as Tools can be developed independently and combined in various configurations to create specialized Agents without rewriting core functionality.

## Tools

Tools are modular, reusable components that enable Agents to perform specific actions or access particular systems. Built on LangChain's Tool framework, each Tool encapsulates a discrete capability such as executing Kubernetes commands, querying observability platforms, or managing cloud resources. Tools can be shared across multiple Agents, promoting code reuse and consistency in functionality. AI Studio provides a library of pre-built Tools for common DevOps tasks while supporting custom Tool development for organization-specific needs.&#x20;

## Builds

The build process transforms Agent definitions and associated Tools into deployable Docker images. During a build, AI Studio pulls the specified base Agent configuration, incorporates selected Tools, and packages everything into a containerized application with standardized API endpoints. Each build generates logs for troubleshooting and validation, and the resulting artifact is versioned for traceability. The build system manages dependencies, ensures proper initialization of language models, and optimizes the final image for performance.&#x20;

## Images

Agent images are Docker Images that encapsulate the AI agent's code, dependencies, etc. &#x20;

## Deployments

Deploying an Agent makes it available for use within your infrastructure. AI Studio streamlines deployment, allowing users to configure resource limits, replica counts, and environment variables to customize behavior. Each deployment is exposed with a Load Balancer and DNS record. &#x20;

## Registration

Registering an Agent connects a deployed agent instance into AI HelpDesk, making it available for user interaction through Tickets. During registration, you provide essential information including the Agent's friendly name, endpoint URL, API path for message handling, and applicable Tenant scopes.&#x20;
