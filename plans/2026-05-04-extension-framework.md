# Extension Framework Documentation Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Create the Extension Framework section in the DuploCloud docs — 13 new markdown files covering the overview, 5-step builder guide, two case studies, and plugin architecture reference — plus SUMMARY.md updates.

**Architecture:** New top-level `extension-framework/` directory with four sub-sections. Content is drawn from three .docx files in the repo root and a plugin architecture design (stored in the design doc). No code — pure markdown documentation.

**Tech Stack:** GitBook-flavored markdown. Diagrams use mermaid code blocks where sequence/state diagrams are needed. No front-matter required unless adding a GitBook `description` field.

---

## Source Files (read before writing any page)

All source material is in `/Users/aboutte/Documents/r/docs/`:

- `plans/2026-05-04-extension-framework-design.md` — approved design (content source mapping table)
- `Replit for Operations_ Build an AI-Powered Enterprise Ops Platform in Days.docx` — Part 3
- `Replit for Operations_ Build an AI-Powered Enterprise Ops Platform in Days (1).docx` — Part 1
- `Replit for Operations_ Build an AI-Powered Enterprise Ops Platform in Days (2).docx` — Part 2

To extract text from a .docx:
```bash
cd /tmp && cp "<path>.docx" doc.docx && unzip -p doc.docx word/document.xml | python3 -c "
import sys, re
content = sys.stdin.read()
text = re.sub(r'<w:br[^/]*/>', '\n', content)
text = re.sub(r'</w:p>', '\n', text)
text = re.sub(r'<[^>]+>', '', text)
text = re.sub(r'\n{3,}', '\n\n', text)
print(text)
"
```

Plugin architecture source is in `plans/2026-05-04-extension-framework-design.md` — but the full design text was provided in the conversation. Key sections: §1 mental model, §2 two contracts, §3 registration, §4–5 storage, §7 authentication, §9 schema lifecycle, §10 lifecycle states.

---

## Task 1: Create Directory Structure and Update SUMMARY.md

**Files:**
- Create: `extension-framework/README.md` (placeholder)
- Create: `extension-framework/building-an-ops-app/README.md` (placeholder)
- Create: `extension-framework/case-studies/README.md` (placeholder)
- Create: `extension-framework/plugin-architecture/README.md` (placeholder)
- Modify: `SUMMARY.md`

**Step 1: Create directory placeholders**

```bash
mkdir -p extension-framework/building-an-ops-app
mkdir -p extension-framework/case-studies
mkdir -p extension-framework/plugin-architecture
touch extension-framework/README.md
touch extension-framework/building-an-ops-app/README.md
touch extension-framework/case-studies/README.md
touch extension-framework/plugin-architecture/README.md
```

**Step 2: Add the section to SUMMARY.md**

Find the line `## Common Use Cases` in `SUMMARY.md` and insert the following block immediately before it:

```markdown
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

**Step 3: Commit**

```bash
git add extension-framework/ SUMMARY.md
git commit -m "chore: scaffold extension-framework directory and SUMMARY.md entries"
```

---

## Task 2: Write `extension-framework/README.md`

**Source:** Part 2 §1–2, Part 3 §2–3, Part 1 §3 (CaaS definition)

**File:** `extension-framework/README.md`

**Required sections and content:**

```markdown
# Extension Framework

Opening paragraph: what it is in one sentence. The Extension Framework lets teams
build domain-specific Ops applications on top of the CaaS platform — applications
that orchestrate existing tool chains (AWS, Salesforce, ServiceNow) through
structured workflows, resource lifecycle management, and AI-powered execution.

## The Three-Layer Stack

Explain the progression:
- Layer 1: CaaS Platform — multiplayer ticketing, connectors, workspaces, RBAC,
  cost management, analytics. A complete product on its own.
- Layer 2: Extension Framework — adds domain-specific orchestration: resource
  taxonomy, dependency enforcement, forms, APIs, status tracking, skills per
  resource type. Built on top of CaaS; all platform capabilities are inherited.
- Layer 3: Developer Experience — build and ship a full Ops application in days
  via the browser or Claude Code. No infrastructure to deploy.

Include the "think of it this way" contrast from Part 2 §1:
  CaaS = users interact through conversations and projects.
  Extension Framework = users interact through forms and structured workflows,
  while AI orchestrates underlying platforms through tickets underneath.

## Why Not Just Use CaaS Directly?

Draw from Part 2 §1 — explain the pattern that emerges with heavy use:
needs are repetitive, natural language becomes laborious, domain-specific
workflows and templates become necessary.

## The Policy Model

This is the core concept (folded in from the dropped core-concepts/ section).

### Resources
Each Ops application manages a taxonomy of domain-specific resources. Examples:
- DevOps: Network, Cluster, Environment, Namespace, Workload
- SalesOps: Cohort, Account, Qualification, Engagement
- SecOps: Policy, Scan, Finding, Remediation

### Spec
What the user provides — the typed input for a resource. Becomes a form in the UI
and an API contract. Example: for a Network, the spec includes region, VPC CIDR,
availability zones, NAT gateway configuration.

### Result
What the agent produces — the typed output captured after execution. Example: for
a Network, the result includes VPC ID, subnet IDs, security groups, route tables.

### Dependencies
Resources form a hierarchy enforced by the framework. A Cluster requires a Network.
An Engagement requires a Qualification. The UI shows only valid options; the
lifecycle respects ordering.

### Skills per Resource Type
Each resource type has a skill associated with it — instructions that tell the agent
how to provision, update, troubleshoot, and deprovision it. The skill is
user-owned, not vendor-hardcoded. Reference the Skills pages in Introduction for
how to write skills.

## What the Framework Provides Automatically

From Part 2 §2 — bullet list:
- Multi-step forms with validation
- REST APIs for every resource type
- List views with status tracking
- Detail views with Spec/Result tabs
- Automatic ticket creation for every provisioning operation
- Cost tracking per resource
- RBAC inherited from workspaces
- "Track Provisioning Status" links to the underlying ticket
- Multiplayer collaboration and audit trails
```

**Step 1: Write the file** using the outline above. Prose, not bullet dumps. Match the tone of existing pages like `introduction/ai-devops-policy-model/README.md`.

**Step 2: Verify** — read the file back, confirm all five sections are present and the policy model (spec/result/dependencies/skills) is clearly explained.

**Step 3: Commit**

```bash
git add extension-framework/README.md
git commit -m "docs: add extension framework overview and policy model"
```

---

## Task 3: Write `building-an-ops-app/README.md`

**Source:** Part 3 §4 intro, Part 2 §6

**File:** `extension-framework/building-an-ops-app/README.md`

**Required sections:**

```markdown
# Building an Ops Application

What this guide covers (one paragraph): walk through the five steps to define,
build, and ship a domain-specific Ops application on the Extension Framework.

## What You'll End Up With

Describe the end state: a running Ops application with forms, status tracking,
AI-powered execution, RBAC, cost management, and audit trails — all inherited
from the CaaS platform. The only work unique to your domain is defining resources
and writing skills.

## Prerequisites

- A DuploCloud account with Extension Framework enabled
- Domain expertise to define your resource taxonomy and write skills
- Provider credentials for the systems you want to orchestrate

## The Five Steps

Brief one-line summary of each step as a numbered list, linking to each step page.
This is an index, not detailed content.
```

**Step 1: Write the file.**

**Step 2: Commit**

```bash
git add extension-framework/building-an-ops-app/README.md
git commit -m "docs: add building an ops app overview page"
```

---

## Task 4: Write the Five Step Pages

Write all five step pages. Each should be 300–600 words. Concrete, instructional tone — not conceptual.

### 4a: `step-1-policy-model.md`

**Source:** Part 3 §4 Step 1, Part 2 §2 (spec/result/dependencies)

Sections:
- What a resource type is
- Defining the Spec (fields, types, what becomes a form)
- Defining the Result (typed output schema)
- Declaring Dependencies (which resources require which)
- Example taxonomy table (DevOps column + SalesOps column side by side)

### 4b: `step-2-skills.md`

**Source:** Part 3 §4 Step 2, Part 1 §7 (intelligence), Part 2 §2 (skills per resource type)

Sections:
- What a skill is in the extension context (a SKILL.md file with instructions for one resource type)
- What to put in the skill (provisioning instructions, scripts, templates, ICP criteria, runbooks — whatever your domain uses)
- Platform skills vs custom skills
- Tip: if the LLM is smart enough to manage a resource from the spec alone, a skill is optional (from Part 2 §2 last paragraph)
- Cross-reference: link to `introduction/ai-devops-policy-model/skills/README.md` for full skill authoring docs

### 4c: `step-3-providers.md`

**Source:** Part 3 §4 Step 3, Part 1 §6 (connectors)

Sections:
- What providers are (any IT system: cloud accounts, CRMs, observability tools)
- Registering a provider and supplying credentials
- Configuring scopes (what the agent can access within the provider)
- Cross-reference: link to `getting-started/integrating-providers/` for provider-specific setup guides

### 4d: `step-4-workspaces.md`

**Source:** Part 3 §4 Step 4, Part 1 §9 (workspaces and RBAC)

Sections:
- Creating a workspace
- Attaching scopes (which systems this workspace's users can access)
- Assigning personas (which skills are available)
- Inviting users and setting RBAC roles
- Example: L1 SRE workspace (read-only infra, write incident management) vs Platform Engineering workspace (full infra write)

### 4e: `step-5-deploy.md`

**Source:** Part 3 §4 Step 5, Part 3 §5 (hosting and deployment)

Sections:
- Your application is live after Step 4 — this step is about choosing how it runs

**Hosted by DuploCloud**
DuploCloud handles deployment, scaling, operations, uptime, and security. Your
application runs in DuploCloud's cloud. Sign up, define your domain, ship.
Best for: getting started, PLG motion, non-sensitive domains.

**Self-Hosted**
Download a Kubernetes manifest with Docker images and run the entire platform in
your own infrastructure. Same application, same capabilities, full control.
Best for: DevOps and SecOps domains where the application operates on production
infrastructure with privileged credentials; regulated industries; organizations
with data residency requirements.

**Step 1: Write all five files.**

**Step 2: Commit**

```bash
git add extension-framework/building-an-ops-app/
git commit -m "docs: add five-step ops app builder guide"
```

---

## Task 5: Write Case Study Pages

### 5a: `case-studies/README.md`

**Source:** Part 2 §5 end (pattern comparison table), Part 2 §6

Short intro (2 paragraphs): what the case studies demonstrate — that the Extension
Framework is domain-agnostic. Same resource model, same ticketing, same skills
execution, same RBAC and cost management. Different domains, identical pattern.

Include the comparison table from Part 2 §5:

| Concept | DevOps | SalesOps |
|---|---|---|
| Resource | Network | Account |
| Spec | Region, CIDR, AZs | Company name, website |
| Skill | CloudFormation template | ICP qualification criteria |
| Provider / Scope | AWS credentials | Apollo API |
| Result | VPC ID, subnets, SGs | Signal verdicts, leads |
| Status | Provisioning → Ready | Processing → Complete |
| Cost tracking | Per resource ($) | Per account ($0.636) |
| Dependency | Cluster needs Network | Engagement needs Qualification |
| Troubleshooting | Track Status → Ticket | Track Status → Ticket |

### 5b: `case-studies/devops-platform.md`

**Source:** Part 2 §4 (full DevOps case study)

Sections:
- **The Policy Model** — table or hierarchy showing Network → Cluster → Environment → (Namespace, Nodes, Workloads, Configs, Storage, Cloud Resources)
- **Creating a Network** — user fills form (name, account/scope, region, VPC CIDR, AZs, NAT gateway, subnet prefix), platform auto-computes subnets, creates provisioning ticket, agent reads skill + spec, plans CloudFormation stack (11 resources), deploys. Completed view shows VPC ID, Overview/Subnets/Routing tabs, Spec/Result tabs, "Track Provisioning Status" link.
- **Creating a Cluster** — dependency enforcement: Network Source field offers "Choose Network" (inherits region/VPC/subnets) or "Choose VPC" (manual). Framework blocks cluster creation without a network.
- **Navigating an Environment** — full resource tree in left nav: Micro Services, Kubernetes (Namespaces, Nodes, Workloads, Configs, Storage, Networks), Cloud Resources (Hosts, Serverless, Storage, Databases, Networks, Configs).
- **Skills in Action** — platform skills like `duplo-aws-infra` contain CloudFormation templates, IAM policies, security group rules. Users can fork and customize.

### 5c: `case-studies/salesops-platform.md`

**Source:** Part 2 §5 (full SalesOps case study)

Sections:
- **The Policy Model** — Demand Gen → Cohort → Account → Qualification → Engagement (with what each represents)
- **How Qualification Works** — agent uses web search + Apollo provider, evaluates ICP signals (Cloud Infrastructure: technologies detected; DevOps Help Needed: job postings; Funding: round and amount). Result: Overall Verdict, extracted leads, signal details, cost ($0.636 example).
- **How Engagement Works** — user selects source sequence from connected sequencing provider (Outreach, Lemlist), multi-step wizard (Sequence, Email & Sender, Leads, Trigger), agent enrolls leads.

**Step 1: Write all three case study files.**

**Step 2: Commit**

```bash
git add extension-framework/case-studies/
git commit -m "docs: add DevOps and SalesOps extension framework case studies"
```

---

## Task 6: Write Plugin Architecture Pages

This sub-section is a technical reference for engineers building plugins. Tone is precise and concrete. Use mermaid diagrams and JSON/code blocks liberally.

### 6a: `plugin-architecture/README.md`

**Source:** Plugin design §1–2

Sections:

**The Mental Model**
The core platform is an operating system; plugins are applications. The OS provides:
window manager (UI shell + menu system), filesystem (namespaced storage), identity
service (authentication, JWTs), package manager (registration, lifecycle, versioning).
Plugins provide their own logic, UI fragments, menu declarations, and data schemas.
A plugin can be written in any language. It only needs to speak HTTP and follow the manifest contract.

**The Two Contracts**

Contract A — What the plugin exposes (inbound):
The plugin must serve the HTTP routes declared in its manifest. Each route is a
menu view (GET, returns HTML) or an action (POST/PUT/PATCH/DELETE). The plugin must
verify the JWT the core sends with every request.

Contract B — What the plugin consumes (outbound):
The plugin calls the core's storage API to persist and read data. It uses a plugin
token issued at registration. It can only touch its own namespaced collections.

Close with: "Everything else — menu rendering, user routing, permission checks,
schema validation, tenant isolation — is the core's responsibility."

### 6b: `plugin-architecture/manifest-and-registration.md`

**Source:** Plugin design §3

Sections:

**The Manifest**
Include the full JSON example from the design:
```json
{
  "plugin_id": "acme-billing",
  "name": "Acme Billing",
  "version": "1.2.0",
  "base_url": "https://acme.example.com/plugin",
  "menu_items": [...],
  "data_schemas": [...]
}
```
Explain each top-level field. Explain menu_items (id, label, view, actions).
Explain data_schemas (collection, schema as JSON Schema, indexes).

**Registration Flow**
Numbered list of what the core does when it receives the manifest:
1. Validates manifest against meta-schema
2. Probes plugin's `/health` endpoint
3. Persists plugin record, menu items, action mappings
4. Provisions MongoDB collections under `plugin_data.{plugin_id}.*`
5. Attaches declared JSON schemas as Mongo `$jsonSchema` validators
6. Builds declared indexes
7. Issues plugin a long-lived plugin token scoped to its namespace

### 6c: `plugin-architecture/storage-api.md`

**Source:** Plugin design §4–5

Sections:

**Namespace Convention**
```
plugin_data.{plugin_id}.{collection}
```
Four properties this gives: isolation, discoverability, schema independence,
migration scoping. Multi-tenant extension: `plugin_data.{tenant_id}.{plugin_id}.{collection}`.

**The API**
Table of the five endpoints:
```
POST   /api/storage/{collection}
GET    /api/storage/{collection}
GET    /api/storage/{collection}/{id}
PATCH  /api/storage/{collection}/{id}
DELETE /api/storage/{collection}/{id}
```

**What the Core Does on Every Call**
Numbered list:
1. Authenticates plugin token
2. Resolves plugin's namespace from token
3. Looks up registered schema for `{collection}`
4. Validates body against schema (rejects if invalid)
5. Executes Mongo operation in namespaced collection
6. Returns result

Close with: "Plugins never construct a database connection, never see Mongo URIs,
never manage their own credentials."

### 6d: `plugin-architecture/authentication.md`

**Source:** Plugin design §7

Sections:

**Three Tokens**
Include the full table from the design:

| Token | Issued to | Carried in | Purpose |
|---|---|---|---|
| User JWT | The user (after login) | Browser cookie / Authorization header to core | Identifies the human |
| Request JWT | Plugin (per request) | Authorization header from core to plugin | Tells the plugin which user is calling and what scopes they have. Short-lived, signed by core. Plugin verifies with core's public key. |
| Plugin token | Plugin (at registration) | Authorization header from plugin to core's storage API | Identifies the plugin to the storage API. Determines which namespace it can touch. |

**Key Rule**
"The user JWT never leaves the browser–core boundary. The request JWT is what the
plugin sees. The plugin token is what the plugin uses to call back. None of them
are interchangeable."

Include the full end-to-end mermaid sequence diagram from the design (§6), adapted
to show where each token appears.

### 6e: `plugin-architecture/lifecycle-states.md`

**Source:** Plugin design §10

Sections:

**State Diagram**
Render the state machine as a mermaid stateDiagram-v2 block:
```
unregistered → registered → active ⇄ degraded
                              ↓
                          disabled → deregistered
                              ↓
                          migrating
```

**State Descriptions**
Table or definition list covering all six states:
- registered — manifest accepted, awaiting first health check
- active — healthy, menus visible, storage open
- degraded — failing health checks; menus hidden, storage open
- disabled — admin-disabled; menus hidden, storage read-only
- migrating — schema migration in progress; menus hidden, storage frozen
- deregistered — removed; data handled per uninstall policy

### 6f: `plugin-architecture/schema-versioning.md`

**Source:** Plugin design §9

Sections:

**Versioning**
Every schema declaration carries a version. The core stores all historical schemas,
not just the latest.

**Compatible Changes** (safe, apply automatically on plugin update):
- Adding optional fields
- Widening enums
- Adding indexes

**Breaking Changes** (require a migration handler):
- Removing fields
- Narrowing types
- Renaming collections

Describe the migration handler flow: plugin registers handler, core calls it on
update, plugin transforms documents in place, plugin is in `migrating` state until
complete.

**Uninstall Policies**
Three policies (core decides per-tenant, plugin has no vote):
- retain — keep data, hide plugin
- archive — move to cold storage
- purge — delete

**Step 1: Write all six plugin architecture files.**

**Step 2: Commit**

```bash
git add extension-framework/plugin-architecture/
git commit -m "docs: add plugin architecture technical reference"
```

---

## Task 7: Final Review and Cleanup

**Step 1: Verify SUMMARY.md links**

Check that every file referenced in SUMMARY.md exists:
```bash
grep -o 'extension-framework/[^)]*' SUMMARY.md | while read f; do
  [ -f "$f" ] && echo "OK: $f" || echo "MISSING: $f"
done
```
Expected: all lines print "OK".

**Step 2: Check for broken internal links**

```bash
grep -r '\[.*\](.*extension-framework' . --include="*.md" | grep -v ".git"
```

Review output for any paths that don't match the file structure.

**Step 3: Final commit if any fixes needed**

```bash
git add -A
git commit -m "docs: fix any broken links in extension framework section"
```

---

## Tone and Style Reference

Match the existing docs voice. Read `ai-dashboards.md` and `introduction/ai-devops-policy-model/README.md` as tone references before writing. Key conventions:
- Lead with what, then how, then why (inverted pyramid)
- Short paragraphs (2–4 sentences)
- Use tables for comparisons, numbered lists for sequential steps, bullets for non-sequential lists
- No marketing language ("powerful", "robust", "seamlessly") — just describe what it does
- GitBook hint blocks (`{% hint style="info" %}`) for tips and cross-references
