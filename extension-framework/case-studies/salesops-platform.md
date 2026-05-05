# AI-Powered SalesOps

To demonstrate that the Extension Framework is domain-agnostic, a second application was built on the same CaaS platform: an AI-powered demand generation platform for sales teams. It uses identical framework mechanics — resource taxonomy, ticket-based execution, cost tracking per resource, RBAC inherited from workspaces — with a completely different domain. There is no infrastructure, no cloud provider, no Kubernetes. There are prospects, campaigns, qualification signals, and outreach sequences.

## The Policy Model

- **Demand Gen** — the top-level container for all sales operations activity.
- **Cohort** — a batch of target accounts grouped for a campaign run (e.g., "May_02"). Tracks total cost across all qualification and engagement activity within it.
- **Account** — a prospective company. The spec is intentionally minimal: company name and website. The framework and skill handle the research from there.
- **Qualification** — AI-powered research and fit analysis. Created automatically when an Account is added to a Cohort. The agent evaluates the account against ICP criteria and returns a structured verdict.
- **Engagement** — outreach execution. The agent selects a sequence template from a connected sequencing provider (Outreach or Lemlist) and enrolls qualified leads. Engagement depends on a completed Qualification — the same dependency enforcement mechanism used in DevOps.

## How Qualification Works

When a user adds an account to a cohort, a Qualification resource is created automatically — no separate action required. The associated skill contains the organization's ICP criteria. The agent researches the prospect using web search and the Apollo provider, evaluating multiple signals in parallel:

- **Cloud Infrastructure** — technologies detected on the company's infrastructure (e.g., AWS, Amazon SES, Route 53, CloudFlare Hosting) → Verdict: PRESENT
- **DevOps Help Needed** — analysis of open job postings; example: 0 DevOps roles hiring → Verdict: LOW
- **Funding** — funding history and recency; example: Series B $31,500,000 (2024), Tier: STRONG → Verdict: STRONG

The result includes an Overall Verdict, a list of extracted leads with contact details, and the full signal breakdown. The ticket sidebar shows the running cost ($0.636 in the example above), company metadata (Industry, Location, Employees), and current status — the same sidebar layout used for every resource across every extension.

## How Engagement Works

For accounts that pass qualification, the user initiates the Engagement stage. A multi-step wizard collects configuration across four steps:

1. **Sequence** — select a source sequence from a connected sequencing provider (Outreach or Lemlist).
2. **Email & Sender** — choose the sending identity and reply-to configuration.
3. **Leads** — confirm which qualified leads to enroll, drawn from the Qualification result.
4. **Trigger** — configure when and how the sequence activates.

The agent then executes the sequence through the connected provider. Like every other resource in the framework, this execution is backed by a ticket — observable in real time, linked from the Engagement detail view, and included in cost tracking.
