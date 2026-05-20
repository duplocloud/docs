---
description: Override default skills and adapt the AWS Extension to your organization's standards.
---

# Customizing the Extension

The AWS Extension ships with production-ready default skills that handle provisioning, updates, and deprovisioning for every resource type. These defaults work out of the box for most teams — but the platform is designed to be fully customizable.

Organizations routinely adapt the extension to enforce:

* **Tagging policies** — require specific tags on all provisioned AWS resources
* **Network topology requirements** — custom CIDR conventions, subnet layouts, or VPC configurations
* **Compliance guardrails** — controls specific to their regulatory environment (SOC 2, HIPAA, PCI-DSS)
* **Architectural standards** — organizational decisions about EKS node types, database configurations, or security settings

Customizations are persistent and survive platform upgrades, because the skill layer is separated from the framework.

## Customization Options

[**Skill Mapping**](skill-mapping.md) — Override the default skill for a specific resource type or ticket origin.
