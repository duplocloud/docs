---
description: 'From Automation to Cognition: Architecting an AI-Native DevOps Platform'
---

# The Problem Statement

**Beyond Personalized Agents: Enterprises DevOps Need Multi-player AI**

Personalized agents like Claude are extraordinary for a single user on a single machine. Enterprise DevOps, is inherently multi-player: shared infrastructure, shared context, and shared accountability across shifts and teams. Converting single player agent to multi-user is a different architecture altogether that brings along a dozen odd new requirements. This blog describes the specifications of such a system.

![](<../.gitbook/assets/Unknown image>)

Historically Ops teams have spent the majority of their time stitching together a sprawling set of tools, to automate an organization’s Business needs. Each tool had its own SME, own interfaces and served a Silo’d functionality. It was left to the operator to bring them together.

Pre-AI tools had two structural failures in their architecture: **rigidity** (every workflow must be anticipated and hardcoded by the vendor) and the **Ops tax** (organizations still needed a large workforce just to configure and operate the software). The advent of ChatGPT and the reasoning capabilities that doubled with every new AI model that followed, opened up an opportunity to truly build a machine that could respond to user requests on the fly w/o users having to build those exact workflows. One could have a software, play the operator’s role i.e. organizations could add an AI Devops Engineer in their workforce that would work side-by-side with humans..

But the industry’s first attempts at AI-native anything, DevOps or otherwise, didn’t get this right.

> <mark style="color:$warning;">**95%**</mark>**&#x20;of enterprise AI pilots had failed till Aug 2025**
>
> <kbd>(MIT study, August 2025)</kbd>

### First **Three AI Approaches Fell Short.**

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>Tack-on AI</strong></p><p>DevOps tools bolted a copilot onto unchanged architecture. AI can’t act beyond that system’s boundaries.</p><p><em>Rigidity isn’t solved — just decorated</em></p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>Wrapper AI</strong></p><p>Startups built thin chat and RAG on foundation models. No multistep workflows, no reasoning. Just a chatbot. Claude ate their lunch.</p><p><em>Storefronts with no differentiator</em></p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>Silo’d AI Ops Tools</strong></p><p>Many startups rebuilt the established categories with AI native technology. AI SRE, AI SIEM, AI for vulnerability checks et al. But we retained the same silos. Many of these tools are beginning to succeed in their own right with better functionality but they do have the same rigidity and lack of interoperability thus a risk of Operators ending up in the same state as before.</p><p><em>Reintroduced the rigidity of past tools</em></p></td></tr></tbody></table>

## Claude Code Changed the Game with a Personalized Agent

While most enterprise AI pilots, with an exception of coding agents like cursor, were failing, Anthropic came with Claude and it instantly showed how AI could solve large swaths of enterprise use cases. AI became mainstream

{% hint style="info" %}
<mark style="color:purple;">**Personalized Agents**</mark> gave engineers a real copilot. It felt like Humans became 10x more productive. One person, one machine, deep focus. Writing code, designing features, prototyping, writing blogs, figuring out complex Kubernetes constructs to deploy an app in the cloud, Claude nailed it. LLM could reason and Agents had all the tools and intelligence to take action on it. The productivity gain with just one agent on an individual's laptop surpassed what dozens of tools cumulatively could achieve.
{% endhint %}

## Managed Agents: Personalized Agents for Autonomous, non-interactive Work

Personalized agents were tied to individual laptops. It seemed obvious that the tasks the agent can execute on an individual’s laptop could be executed in the cloud. They could be uninterrupted, run on a schedule, use bigger cloud resources and centralized system credentials. Claude formalized this need with the launch of Managed Agents.

{% hint style="info" %}
The primary purpose of Managed Agent is to run repeatable jobs autonomously w/o interruptions., They scale the capabilities of a personalized agent using cloud infrastructure that could run a swarm of them doing repeatable compute intensive tasks. They are still architecturally a single-user system.
{% endhint %}

An example application of Managed Agents is incident triaging. Triggered via webhook when an incident is logged in an Incident Management system, the agent triages it and updates its findings for the human to review and then take action.

## Enterprise Ops needs are inherently Multi-player

How many times would we have wished that you could do a live share of our Claude code session?

_An incident at 2 AM diagnosed by one on-call SRE must hand off full context — pod state, CPU and memory utilization, actions already taken, rollback attempts — to the morning shift. A multi-step cloud migration requires centralized coordination across many tasks. Top of the wish list is being able to add colleagues in the same Claude session._

A large shared infrastructure, dozens of engineers, shared state, access control across environments, audit trails for compliance, deterministic deployments, and a cost model that doesn’t scale linearly with every kubectl command, the Single player agent model is simply built for it.

|                                                                                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><mark style="color:green;"><strong>Single-player ✓</strong></mark></p><p>Helping a user write code, designing deployments, prototyping. One person, one machine, deep focus. Claude Code nails this.</p><p>Autonomous agents auto-triaging, remediating incidents with no humans in the loop. Managed agents nail this.</p> | <p><mark style="color:red;"><strong>Operations (multi-player) ✗</strong></mark></p><p>Humans and agents need to collaborate: migrations, troubleshooting incidents, coordinating deployments. Shared systems, shared context, shared accountability.<br><br><br></p> |

Using desktop agents for infrastructure operations means the same diagnostic questions get asked repeatedly across the organization. There is no organizational memory, no collaboration, no compounding intelligence. The SRE on the night shift discovers the root cause of a pod crash loop. The morning engineer asks Claude Code the same question from scratch. The context stays local to each machine and vanishes when the session ends.

{% hint style="info" %}
**Token cost of every user running their own desktop session for the same repetitive Ops workflows is financially unsustainable at enterprise scale**
{% endhint %}

If you were to imagine a multiplayer Agent, what would it look like? The table below is the capability matrix between the 3 models. The features the multi-player Agent that would implement all the features of personalized and Managed agent cemented by the feature set needed to make it Multi-player.

|                                    | Personalized | Managed | Multi-player |
| ---------------------------------- | ------------ | ------- | ------------ |
| Reasoning Capabilities             | ✅            | ✅       | ✅            |
| Tools                              | ✅            | ✅       | ✅            |
| Hosted Service                     | ❌            | ✅       | ✅            |
| Long Autonomous Tasks              | ❌            | ✅       | ✅            |
| Interactive                        | ✅            | ❌       | ✅            |
| Multi-user Session                 | ❌            | ❌       | ✅            |
| Centralized Context                | ❌            | ✅       | ✅            |
| Enterprise RBAC                    | NA           | ❌       | ✅            |
| Shared Secrets                     | NA           | ✅       | ✅            |
| Workspaces and Resource Management | NA           | ❌       | ✅            |
| Safety and Security                | NA           | NA      | ✅            |

## Enterprise Operations is further specialized, it needs all 3 and more

Once you make any software multiplayer that opens up a pandora’s box. We now need to worry about a vast set of functionality stemming from the fact that no one individual is now accountable for the agent’s action. We identify and summarize twelve capabilities that any AI-native Ops platform must provide.

Ironically each one exists in traditional Saas tooling. None of them exist in today’s AI tools. They must be architected from the ground up for AI.

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>1. Multiplayer AI Sessions</strong></p><p>A production incident might span an on-call SRE, a platform engineer, a database administrator, and a team lead — across multiple shifts over 48 hours. The state of the cluster when each person touched it, the commands they ran, the hypotheses they tested — all of this context must flow between participants. When the morning engineer picks up an incident, the AI should already know: here’s the pod state at 2 AM, here’s what the on-call tried, here’s what worked and what didn’t.</p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>2. Centralized Context</strong></p><p>When a developer asks Claude Code “why is this service failing?” the agent investigates from scratch — every time. It has no memory that the same question was asked yesterday, that the root cause was a DNS misconfiguration in the service mesh, or that this service has a history of OOM kills during peak traffic. An AI-native DevOps platform must centralize all context — every session, every infrastructure change, every incident resolution — into a shared knowledge layer that compounds over time.</p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>3. Enterprise RBAC</strong></p><p>There is no way to define that a junior developer can deploy to staging but not production. No way to ensure an application team sees their own namespace but not the platform team’s infrastructure. No way to restrict which clusters, cloud accounts, or secrets an agent can touch. SOC 2, HIPAA, PCI-DSS — regulated industries can’t even evaluate a tool that lacks access control.</p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><strong>4. Determinism and SLAs</strong><br>The same prompt can produce different Terraform plans on different runs. For a sandbox, acceptable. For a production Kubernetes upgrade, a non-starter. The determinism must be customizable: a deployment to production always follows the blue-green sequence. A database migration always takes a snapshot first. The AI reasons freely when diagnosing, executes predictably when deploying — and the boundary is in the team’s hands, not the vendor’s.</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>5. Templates for Repetitive Tasks</strong></p><p>If a team deploys the same application stack to staging three times a week, that shouldn’t be a prompt every time. It should be a template — a pre-configured workflow that captures the intent once and executes it on demand. Typing a prompt is powerful for novel troubleshooting. It’s a regression from a one-click button for the deployment you run twenty times a day.</p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>6. Alerts and Notifications</strong></p><p>A deployment fails — the team gets paged. A node runs out of disk — the platform team is alerted. A Terraform drift is detected — the compliance lead is notified. AI tools today are entirely reactive. They have no concept of proactive monitoring, threshold-based alerts, or notification routing to the right engineer through PagerDuty or Slack.</p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>7. Fault Handling and Retries</strong></p><p>Cloud API calls time out. Models hallucinate a kubectl command that doesn’t exist. AWS throttles an API. In a platform running hundreds of concurrent infrastructure workflows, manual retries don’t scale. Automatic retries with exponential backoff, circuit breakers, fallback strategies, and clear escalation paths when automated recovery fails. An AI agent that silently drops a deployment step is worse than one that never ran.</p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>8. Scale and Performance</strong></p><p>Claude Code runs on a developer’s laptop. It serves one user at a time. A DevOps platform serves hundreds of concurrent engineers, each running workflows that involve multiple AI interactions, tool calls, and cloud API invocations. The agents must run in the cloud, not on laptops — orchestrated, load-balanced, and monitored like any production service.</p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>9. Resource Management and Workspaces</strong></p><p>A DevOps platform needs workspaces that map to organizational structures — separating production from staging, isolating one team’s cluster from another’s, providing boundaries that prevent one group’s AI operations from affecting another’s infrastructure.</p></td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>10. Security</strong></p><p><strong>Token and credential safeguarding</strong> AWS access keys, Kubernetes service account tokens, Vault secrets — guaranteed never leaked through AI responses or exfiltrated through prompt manipulation.</p><p><strong>Prompt injection defense</strong> Malicious inputs in Helm values files, ConfigMaps, or pod annotations that could manipulate an agent into bypassing RBAC or running destructive commands.</p><p><strong>Sandboxing</strong> An agent diagnosing a production issue should not be able to accidentally delete a persistent volume unless explicitly authorized.</p><p><strong>Impersonation controls</strong> Every AI action traceable to a specific user, governed by their access scope — not elevated system-level access.</p></td></tr></tbody></table>

<table><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>11. Token Cost Management</strong></p><p>In a DevOps organization with a hundred engineers running concurrent infrastructure workflows, the token bill becomes the single biggest line item in the AI budget.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Token cost with desktop agents is not a pricing problem — it’s an <strong>architectural limitation</strong>. We’ve seen organizations prototype AI-native infrastructure workflows, validate the value, and then abandon them when they project the cost of running them at scale.</p></div></td></tr></tbody></table>

<table><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td></td><td><p><strong>12. Token-less Analytics</strong></p><p>Fifty engineers checking the same deployment status dashboard means fifty inference cycles for identical information. This is architecturally absurd.</p><div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>AI should <strong>create</strong> the dashboard — generate the Prometheus query, build the visualization. It shouldn’t be <strong>running</strong> the dashboard. The intelligence is in the design, not in the rendering. This is what we call <strong>token-less analytics</strong>: AI-generated artifacts that run without AI.</p></div></td></tr></tbody></table>

## **The Gap is the Opportunity**

Twelve requirements. Every one of them has existed in present-day Operations software. We need to take the power of personalized agents and scale them to the enterprise use case — without introducing the rigidity of SaaS tools and without recreating the siloed tool chain we’re trying to escape.

This is what DuploCloud AI DevOps Platform implements.
