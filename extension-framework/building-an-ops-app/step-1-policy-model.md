# Step 1: Define Your Policy Model

The policy model is the taxonomy of resources your application manages. Everything else — forms, APIs, status tracking, dependency enforcement — is generated from it. Before writing a single skill or registering a provider, you need to decide what objects your domain operates on and how they relate to each other.

## Resource Types

A resource type is the fundamental unit of your policy model. It represents a distinct, manageable object in your domain: a Network, a Cluster, an Account, a Qualification. Each resource type defines four things: a name, a spec (the typed input the user provides), a result (the typed output the agent produces), and optionally a set of dependencies on other resource types. The framework uses these definitions to generate forms, API endpoints, list views, and detail views automatically — no additional UI work required.

## Defining the Spec

The spec captures what the user wants. It is a typed set of fields that the user fills out when creating or updating a resource. When you define the spec for a resource type, those fields become a validated form in the UI and an API contract for programmatic access.

The fields in a spec should reflect exactly what the agent needs to do its job. For a **Network**, the spec includes region, VPC CIDR, availability zones, whether to provision a NAT gateway, and a subnet prefix — the platform auto-computes the individual subnets from the CIDR and displays them in a table before the user confirms. For a **Sales Account**, the spec is minimal: company name and website. The agent can derive everything else from those two inputs using connected providers and web research.

Fields have names, types, and optional validation rules. Keep specs as narrow as possible — fields the agent can infer or compute should not be user-facing inputs.

## Defining the Result

The result captures what the agent produced. It is the typed output that the agent writes when it finishes provisioning or updating a resource. The framework reads this output, parses it into the resource's typed Result, and displays it in the detail view alongside the original Spec.

For a **Network**, the result includes the VPC ID, subnet IDs, security group identifiers, and route table references — the concrete infrastructure artifacts that downstream resources (Clusters, Environments) will depend on. For a **Sales Account qualification**, the result includes a structured signal analysis (cloud infrastructure detected, funding tier, hiring signals), an overall fit verdict, and the extracted leads that the Engagement stage will use.

Define result fields to match what downstream resources will consume as inputs — this is what makes the dependency chain work.

## Declaring Dependencies

Resource types can declare that they depend on other resource types. The framework enforces these dependencies at every layer: the UI shows only valid options when a dependency must be selected, and the lifecycle prevents a dependent resource from being provisioned until its dependencies are in the `Ready` state.

For example, a **Cluster** declares a dependency on **Network** — the cluster creation form presents a "Network Source" field where the user selects from provisioned networks, and region, VPC, and subnet configuration are inherited automatically. An **Engagement** declares a dependency on **Qualification** — engagement forms show only accounts whose qualification has completed with a suitable verdict.

Dependencies also determine teardown order: the framework will not deprovision a Network while a Cluster that depends on it is still live.

## Example Taxonomies

The same pattern applies across different domains. The table below shows how a DevOps taxonomy and a SalesOps taxonomy map to the same five levels of hierarchy:

| Level | DevOps | SalesOps |
|-------|--------|----------|
| 1 | Network | Demand Gen |
| 2 | Cluster | Cohort |
| 3 | Environment | Account |
| 4 | Namespace / Workload | Qualification |
| 5 | — | Engagement |

In both cases, each level depends on the one above it. The framework enforces the ordering; you just declare the structure.
