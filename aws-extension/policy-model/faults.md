---
description: >-
  Cross-resource issues detected across the AWS Extension hierarchy — surfaced
  with severity, context, and links to the originating ticket.
---

# Faults

Faults are issues detected by the platform across any resource in the AWS Extension — Networks, Clusters, Environments, workloads, or databases. They are surfaced centrally so teams can see and act on problems without hunting through individual resource views.

Each Fault captures what went wrong, how severe it is, which resource is affected, and when it was detected. Where the fault originated from a ticket execution, a direct link to that ticket is included.

## Severity Levels

| Severity | Description |
|---|---|
| **Info** | Informational — no immediate action required |
| **Warning** | Something is degraded or suboptimal, but the resource is still functional |
| **Error** | The resource has encountered a problem that requires attention |
| **Critical** | A severe issue that may be causing an outage or data loss |

## Fault Details

Each Fault includes:

| Field | Description |
|---|---|
| **Message** | A description of the issue |
| **Severity** | Info, Warning, Error, or Critical |
| **Resource** | The resource type, ID, and name the fault is attached to |
| **Detected At** | When the fault was first detected |
| **Details** | Additional context or diagnostic information |
| **Ticket** | A link to the ticket that triggered or detected this fault, if applicable |

## Where Faults Appear

Faults are visible in the **Faults** view, which aggregates issues across all resource types in the workspace. Individual resource detail pages also surface any active faults attached to that specific resource.

## What's next

Return to the [Policy Model overview](README.md) to explore the full resource hierarchy.
