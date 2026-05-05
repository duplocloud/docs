# Step 2: Write Your Skills

A skill tells the agent how to provision, update, troubleshoot, and deprovision a specific resource type. Skills encode your domain expertise — runbooks, ICP criteria, CloudFormation templates, API sequences — as instructions the agent can follow. If your operational knowledge lives in a wiki, in someone's head, or in a folder of scripts, it belongs in a skill.

## What a Skill Is

A skill is a folder containing a `SKILL.md` file with metadata and instructions. Optionally it includes supporting assets: shell scripts, CloudFormation or Terraform templates, reference materials, API schemas, or any other artifacts the agent should use during execution. The skill is the atomic unit of business logic in the Extension Framework — it is user-owned, version-controlled, and modifiable without waiting for a vendor release.

When the framework creates a provisioning ticket for a resource, it resolves the skill associated with that resource type and stages the skill files in the ticket's working directory before the agent begins. The agent reads the skill instructions, reads the resource spec, and executes accordingly.

## What to Put in a Skill

The content of a skill depends entirely on the resource type and how deterministic you need the agent's behavior to be.

For a **Network** resource, the skill might contain a CloudFormation template that defines the VPC, subnets, route tables, internet gateway, and NAT gateway — along with IAM policy definitions and tagging standards the organization requires. The agent reads the template, parameterizes it from the spec, and deploys it via the AWS provider.

For a **Sales Qualification** resource, the skill contains the organization's Ideal Customer Profile criteria: firmographic signals to check, funding tiers that indicate fit, hiring patterns that suggest active need, technology signals that indicate relevance. The agent uses these criteria to evaluate the prospect against data from connected providers (Apollo) and web research.

For a **Compliance Policy** resource, the skill might contain control definitions, evidence collection procedures, and instructions for which provider APIs to query when gathering audit artifacts.

In every case, the skill is the place where your organization's specific standards, thresholds, and procedures live — not in the platform's source code.

## Platform Skills vs. Custom Skills

There are three categories of skills:

**Platform skills** ship pre-built with the Extension Framework. They cover common operational patterns: project management workflows, dashboard creation, troubleshooting patterns, and provider-specific infrastructure templates like `duplo-aws-infra`. Platform skills are a starting point — your team can fork any platform skill and customize it to add your own tagging policies, compliance requirements, or architectural standards.

**Custom skills** are written by your own team. They encode workflows, policies, and operational practices that are specific to your organization. Custom skills are where competitive differentiation lives — the ICP criteria that your sales VP has refined over years, the deployment runbook your senior SRE wrote, the compliance checklist your auditor follows.

**External skills** are third-party skill packages from vendors such as Pulumi, HashiCorp, or cloud providers. They extend the agent's capabilities for specific tool chains without requiring custom development.

## Skills Are Optional

A skill is not required for every resource type. LLMs are capable enough that for many resource types — particularly those with straightforward specs and well-known underlying platforms — the agent can manage the resource from the spec alone, using its own knowledge of the target system.

Add a skill when you need one or more of the following: determinism (the agent must follow a specific script or use a specific template), domain-specific knowledge the LLM does not have out of the box (proprietary ICP criteria, internal naming conventions, organization-specific compliance controls), or custom scripts the agent should execute rather than reason from scratch.

If the resource type is simple and the LLM handles it well without guidance, a skill is not necessary.

{% hint style="info" %}
For full skill authoring documentation — including `SKILL.md` schema, supported asset types, versioning, and skill testing — see [Skills in the Introduction](../introduction/ai-devops-policy-model/skills/README.md).
{% endhint %}
