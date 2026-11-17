---
description: Pick the platform you work on and follow a worked example that ends in an agent you built yourself.
---

# Build Your Own Agent

Each example below is a follow-along walkthrough. It takes a couple of hours, needs as little access as possible (for example, read-only on AWS), and ends in a working agent in your DevKit. Pick the one that matches where you work.

| Platform | Example |
| --- | --- |
| [AWS](aws.md) | A security agent that checks your account |
| [Azure](azure.md) | A security agent that checks your subscription |
| [GCP](gcp.md) | A security agent that checks your project |
| [Kubernetes](kubernetes.md) | An agent that works on your cluster |
| [Git](git.md) | A pull-request code-review agent |
| [Other tools](other.md) | A Jira or CI pipeline agent |

## How you build an agent

Every example follows the same three steps:

1. **Write a spec.** Say what the agent should do, what it can touch, and what it must never do.
2. **Describe the experience.** Decide what the user sees: a chat, a form, a dashboard, or a mix.
3. **Build it.** Use the DevKit and Claude Code to turn the spec and the experience into an agent, then test it against your own account.

You need the DevKit running first. If you haven't installed it yet, start with [Install the DevKit](../install-the-devkit.md).
