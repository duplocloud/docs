# Extension Framework Documentation — Design

**Date:** 2026-05-04
**Status:** Approved

## Goal

Add a new top-level "Extension Framework" section to the DuploCloud docs covering the three-layer CaaS stack: the platform foundation (Part 1), the Extension Framework for building Ops applications (Part 2), and the developer experience for shipping apps in days (Part 3). Also document the plugin architecture technical spec.

## Source Material

| File | Content |
|---|---|
| `Replit for Operations_ Build an AI-Powered Enterprise Ops Platform in Days.docx` | Part 3 — developer experience, 5-step build process, hosting options, GTM |
| `Replit for Operations_ Build an AI-Powered Enterprise Ops Platform in Days (1).docx` | Part 1 — CaaS architecture, ticketing, connectors, skills, workspaces, RBAC, cost |
| `Replit for Operations_ Build an AI-Powered Enterprise Ops Platform in Days (2).docx` | Part 2 — Extension Framework, policy model, resource lifecycle, DevOps & SalesOps case studies |
| Plugin Architecture design (user-provided) | Technical spec: manifest, storage API, authentication, lifecycle states, schema versioning |

## Approved Structure

### File Layout

```
extension-framework/
├── README.md                          # Overview, three-layer stack, policy model concepts
├── building-an-ops-app/
│   ├── README.md                      # Builder overview
│   ├── step-1-policy-model.md         # Define resource types and dependencies
│   ├── step-2-skills.md               # Write skills for each resource type
│   ├── step-3-providers.md            # Connect providers and configure scopes
│   ├── step-4-workspaces.md           # Create workspaces, assign scopes/personas, invite users
│   └── step-5-deploy.md              # Hosted by DuploCloud vs. self-hosted Kubernetes manifest
├── case-studies/
│   ├── README.md                      # Why two domains, what they prove
│   ├── devops-platform.md             # Network → Cluster → Environment → Workloads
│   └── salesops-platform.md          # Cohort → Account → Qualification → Engagement
└── plugin-architecture/
    ├── README.md                      # Mental model (OS/app analogy) + two contracts
    ├── manifest-and-registration.md   # Manifest schema, registration flow, health probe
    ├── storage-api.md                 # Generic CRUD API, namespacing, schema validation
    ├── authentication.md              # Three tokens: user JWT, request JWT, plugin token
    ├── lifecycle-states.md            # State machine + transitions
    └── schema-versioning.md           # Compatible vs. breaking changes, migrations, uninstall policies
```

### SUMMARY.md Placement

After "Getting Started", before "Common Use Cases":

```
## Extension Framework

* [Overview](extension-framework/README.md)
* [Building an Ops Application](extension-framework/building-an-ops-app/README.md)
  * [Step 1: Define Your Policy Model](extension-framework/building-an-ops-app/step-1-policy-model.md)
  * [Step 2: Write Your Skills](extension-framework/building-an-ops-app/step-2-skills.md)
  * [Step 3: Connect Providers](extension-framework/building-an-ops-app/step-3-providers.md)
  * [Step 4: Configure Workspaces](extension-framework/building-an-ops-app/step-4-workspaces.md)
  * [Step 5: Deploy](extension-framework/building-an-ops-app/step-5-deploy.md)
* [Case Studies](extension-framework/case-studies/README.md)
  * [AI-Native DevOps Platform](extension-framework/case-studies/devops-platform.md)
  * [AI-Powered SalesOps](extension-framework/case-studies/salesops-platform.md)
* [Plugin Architecture](extension-framework/plugin-architecture/README.md)
  * [Manifest & Registration](extension-framework/plugin-architecture/manifest-and-registration.md)
  * [Storage API](extension-framework/plugin-architecture/storage-api.md)
  * [Authentication](extension-framework/plugin-architecture/authentication.md)
  * [Lifecycle States](extension-framework/plugin-architecture/lifecycle-states.md)
  * [Schema Versioning](extension-framework/plugin-architecture/schema-versioning.md)
```

## Content Source Mapping

| Page | Primary source |
|---|---|
| `README.md` | Part 3 §2 (vision), Part 2 §1 (what Extension Framework adds), Part 2 §2 (policy model concepts) |
| `building-an-ops-app/README.md` | Part 3 §4 intro, Part 2 §6 (what this means) |
| `step-1-policy-model.md` | Part 3 §4 Step 1, Part 2 §2 (spec, result, dependencies) |
| `step-2-skills.md` | Part 3 §4 Step 2, Part 1 §7 (intelligence/skills) |
| `step-3-providers.md` | Part 3 §4 Step 3, Part 1 §6 (connectors) |
| `step-4-workspaces.md` | Part 3 §4 Step 4, Part 1 §9 (workspaces and RBAC) |
| `step-5-deploy.md` | Part 3 §4 Step 5 + §5 (hosting options) |
| `case-studies/devops-platform.md` | Part 2 §4 |
| `case-studies/salesops-platform.md` | Part 2 §5 |
| `plugin-architecture/README.md` | Plugin design §1–2 (mental model, two contracts) |
| `plugin-architecture/manifest-and-registration.md` | Plugin design §3 |
| `plugin-architecture/storage-api.md` | Plugin design §4–5 |
| `plugin-architecture/authentication.md` | Plugin design §7 |
| `plugin-architecture/lifecycle-states.md` | Plugin design §10 |
| `plugin-architecture/schema-versioning.md` | Plugin design §9 |

## Open Questions (deferred)

- Where does Part 1 CaaS architecture content (ticketing internals, credential translation, session isolation, sandboxing) live? Options: fold into `README.md` as a "How the platform works" section, or add a separate `platform-architecture.md` page.
- Should the case studies directory include a comparison table page (Part 2 §5 table showing DevOps vs. SalesOps pattern equivalence)?
