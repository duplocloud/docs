# Case Studies

The following case studies show the Extension Framework in action across two production applications. Their purpose is to make one point concrete: the framework is domain-agnostic. The resource model, the ticketing system, the skill-driven execution engine, the RBAC, and the cost management system are all shared infrastructure. What differs between applications is only the policy model — the resource taxonomy — and the skills that encode each domain's operational logic.

The two applications covered here could not be more different. One automates cloud infrastructure: VPCs, Kubernetes clusters, IAM roles, and workloads. The other automates sales demand generation: prospect cohorts, ICP qualification, and outreach sequencing. Both were built on the same CaaS platform, using identical framework mechanics. A team that understands how one application works can read the other and recognize every pattern immediately.

## The Pattern

The table below maps the same conceptual framework elements across both domains. Every column is the same object — only the domain-specific label and content change.

| Concept | DevOps | SalesOps |
| --- | --- | --- |
| Resource | Network | Account |
| Spec | Region, CIDR, AZs | Company name, website |
| Skill | CloudFormation template | ICP qualification criteria |
| Provider / Scope | AWS credentials | Apollo API |
| Result | VPC ID, subnets, SGs | Signal verdicts, leads |
| Status | Provisioning → Ready | Processing → Complete |
| Cost tracking | Per resource | Per account ($0.636 example) |
| Dependency | Cluster needs Network | Engagement needs Qualification |
| Troubleshooting | Track Status → Ticket | Track Status → Ticket |

Two completely different operational domains, one framework, one platform. See the [AI-Native DevOps Platform](devops-platform.md) case study for a detailed walkthrough of cloud infrastructure automation, and the [AI-Powered SalesOps](salesops-platform.md) case study for demand generation.
