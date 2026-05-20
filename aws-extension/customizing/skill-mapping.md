---
description: Override the default provisioning skill for a specific resource type with a custom skill.
---

# Skill Mapping

Skill Mapping lets you override the platform default skill for a specific ticket origin and sub type. When a ticket is created that matches the override, the AI agent loads your custom skill instead of the platform default — without any change to the resource configuration or ticket setup.

For the AWS Extension, this means you can replace the default AWS infrastructure provisioning skill with one that incorporates your organization's specific requirements: custom tagging, different CloudFormation templates, additional compliance checks, or modified approval workflows.

## How it works

The platform default skill for AWS infrastructure provisioning is **duplo-aws-infra**. It handles provisioning and deprovisioning for Networks, Clusters, and Environments. When a provisioning ticket is created for any of these resource types, the agent loads this skill automatically.

With Skill Mapping, you can:

* Create a custom skill that extends or replaces `duplo-aws-infra`
* Map it as an override for a specific resource type (e.g. Network Baseline provisioning only)
* All subsequent provisioning tickets for that resource type will use your custom skill instead

The platform default continues to apply to any resource type without an override.

## Setting up a Skill Mapping Override

For the full step-by-step guide, see [Platform Skills and Overrides](../../armor/skills/platform-skills-and-overrides.md).

{% content-ref url="../../armor/skills/platform-skills-and-overrides.md" %}
[platform-skills-and-overrides.md](../../armor/skills/platform-skills-and-overrides.md)
{% endcontent-ref %}

## Example: Enforcing a Tagging Policy

Your organization requires that all AWS resources are tagged with `team`, `cost-center`, and `environment`. The platform default skill does not know about these requirements.

{% stepper %}
{% step %}
## Fork the default skill

Copy the `duplo-aws-infra` skill and add tagging instructions to the network and cluster provisioning sections.
{% endstep %}

{% step %}
## Add a Skill Mapping override

Navigate to **AI Admin → Skills → Skill Mapping** and add an override mapping the Network Baseline and Cluster Baseline origin types to your custom skill.
{% endstep %}

{% step %}
## Verify

Create a new Network Baseline provisioning ticket. The agent loads your custom skill and enforces the tagging requirement during provisioning.
{% endstep %}
{% endstepper %}
