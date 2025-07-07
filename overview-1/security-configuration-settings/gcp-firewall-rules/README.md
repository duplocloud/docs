---
description: Configure firewall rules in DuploCloud for GCP environments
---

# GCP Firewall Rules

Firewall rules in Google Cloud Platform (GCP) control inbound and outbound network traffic to your virtual machines and other cloud resources. These rules define whether traffic is allowed or denied based on source IP ranges, protocols, ports, and targets.

DuploCloud enables you to manage GCP firewall rules directly from the Portal. Firewall rules are stateful, meaning return traffic is automatically allowed for approved inbound connections.

There are two types of firewall rules in DuploCloud:

* [Infrastructure Firewall Rules](infrastructure-firewall-rules.md): Apply to an entire GCP infrastructure environment. Ideal for managing baseline network access at the environment level.
* [Tenant-Based Firewall Rules](tenant-based-firewall-rules.md): Apply to individual tenants within an infrastructure. Useful for isolating tenant workloads or defining tenant-specific traffic policies.
