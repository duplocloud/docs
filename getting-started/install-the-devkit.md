---
description: Download the DuploCloud DevKit and start building agents on your own machine.
---

# Install the DevKit

The DevKit runs the DuploCloud platform on your own machine in containers. You use it to connect your cloud accounts, ask the AI agent questions about them, and build your own agents, which load into the running platform without a restart.

The DevKit is public on GitHub at [duplocloud/devkit](https://github.com/duplocloud/devkit). Its docs are the full, step-by-step guide. This page gives you the overview and links to the right place for each step.

## What you need

* A container runtime with Compose v2 (Docker or podman).
* Python 3.
* Access to an LLM: an Anthropic API key, AWS Bedrock credentials, or an Anthropic-compatible LLM gateway.
* An email address you can read right away. Work or personal addresses are fine. Privacy-relay and disposable addresses are not accepted.
* A few free local ports.

The details, including podman on Apple Silicon, are in [Prerequisites](https://github.com/duplocloud/devkit/blob/main/docs/getting-started/prerequisites.md). On Windows, set up WSL 2 first: [Windows: set up WSL](https://github.com/duplocloud/devkit/blob/main/docs/getting-started/windows-wsl.md).

## What happens on first run

You clone the repository and run its start script. The commands are in [Install and sign in](https://github.com/duplocloud/devkit/blob/main/docs/getting-started/install.md).

1. **You enter an admin email.** This becomes your login for the local portal.
2. **DuploCloud requests a trial license for that email** and sends you a verification link. The run waits for you to click it, then continues on its own. If the wait times out, click the link anyway and run the script again; it picks up the same request.
3. **You set a password and choose your LLM provider.** The script then starts the platform and creates a workspace for you to build in.
4. **You sign in** to the portal at `http://localhost:4210`.

{% hint style="warning" %}
DuploCloud issues **one license per email address**. The DevKit reuses or recovers the license it already has, so you shouldn't need another. If you already hold a license token, pass it with `--license <jwt>` to skip the trial request. To renew an expired trial, contact **sales@duplocloud.net**.
{% endhint %}

How the DevKit handles licenses is in [Configuration: Licensing](https://github.com/duplocloud/devkit/blob/main/docs/configuration.md#licensing). For how licenses work across DuploCloud, see [License](licensing.md).

## Where the DevKit stores things

Everything stays on your machine, in the folder you cloned:

| What | Where |
| --- | --- |
| Settings, credentials and your license token | The `.env` file |
| Your agents | `extensions/<name>/`. Upgrades and resets never touch this folder. |
| Platform data: database, file store, search index and loaded agents | Container volumes |

Stopping the DevKit keeps your data. Some reset commands delete the volumes but keep your license. [What each command destroys](https://github.com/duplocloud/devkit/blob/main/docs/cli-reference.md#what-each-command-destroys) lists exactly what each one removes.

## Where to go next

| To do this | Read |
| --- | --- |
| Connect an AWS account and ask the agent about it | [Connect AWS](https://github.com/duplocloud/devkit/blob/main/docs/getting-started/connect-aws.md) |
| Connect a Kubernetes cluster | [Connect Kubernetes](https://github.com/duplocloud/devkit/blob/main/docs/getting-started/connect-kubernetes.md) |
| Build your first agent | [Build your first extension](https://github.com/duplocloud/devkit/blob/main/docs/getting-started/build-your-first-extension.md) |
| Get a working setup fast | [Quickstart](https://github.com/duplocloud/devkit/blob/main/docs/quickstart.md) |
| Upgrade to a newer DevKit | [Upgrading](https://github.com/duplocloud/devkit/blob/main/docs/upgrading.md) |
| Fix a problem | [Troubleshooting](https://github.com/duplocloud/devkit/blob/main/docs/troubleshooting.md) and the [FAQ](https://github.com/duplocloud/devkit/blob/main/docs/faq.md) |
| Look up a command or flag | [CLI reference](https://github.com/duplocloud/devkit/blob/main/docs/cli-reference.md) |

When your agents are ready, [deploy your portal](installation/README.md) to your cloud and [deploy your own agents](deploy-your-own-agents.md) to it.
