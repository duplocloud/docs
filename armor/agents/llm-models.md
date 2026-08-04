# LLM Models

The **LLMs** section governs which models are available to agents, and which model a Workspace, Project, or the platform as a whole uses by default. It's reached from **AI Admin → LLMs**, and has three tabs: **Agent SDKs**, **LLMs**, and **LLM Mappings**.

![LLMs tab — the model registry](../../../.gitbook/assets/llm-models-step-01-overview.png)

## Agent SDKs

An **Agent SDK** is a connection to a deployed agent runtime — the same entity described in [Adding a Custom Agent](README.md#adding-a-custom-agent): a Name, Description, Endpoint, and Path. It's listed here because every model in the registry is registered under one.

![Agent SDKs tab](../../../.gitbook/assets/llm-models-step-02-agent-sdks-tab.png)

Click **+ Add** to register another one.

![Add Agent SDK form](../../../.gitbook/assets/llm-models-step-03-add-sdk-empty.png)

![Add Agent SDK form filled in](../../../.gitbook/assets/llm-models-step-04-add-sdk-filled.png)

![Agent SDK added](../../../.gitbook/assets/llm-models-step-05-sdk-added.png)

## LLMs

The **LLMs** tab is the model registry itself — every model an agent is allowed to use, paired with the Agent SDK(s) that can run it.

Click **+ Add** and fill in:

* **Agent SDKs\*** — which SDK(s) this model can run under
* **Model ID\*** — the underlying model identifier (e.g. `claude-sonnet-5`)
* **Display Name\*** — a human-readable name shown in ticket creation and elsewhere (e.g. `Sonnet 5`)
* **Description** — optional
* **Enabled** — toggle it off to keep a model registered but unavailable for selection

![Add Model form](../../../.gitbook/assets/llm-models-step-06-add-model-empty.png)

![Add Model form filled in](../../../.gitbook/assets/llm-models-step-07-add-model-filled.png)

![New model in the registry](../../../.gitbook/assets/llm-models-step-08-model-added.png)

{% hint style="info" %}
This registry doesn't have a "Provider" field — it doesn't matter here whether a model runs on AWS Bedrock, GCP Vertex AI, Azure AI Foundry, or directly against the Anthropic API. That's determined by environment variables on the Agent SDK's own deployment, not by anything you configure in this UI.
{% endhint %}

## LLM Mappings

A **Mapping** controls which registered models are actually usable — and which one is the default — for a given scope. This is what makes the registry an *allow-list*: if no mapping covers a workspace, no models are available to it at all.

![LLM Mappings tab](../../../.gitbook/assets/llm-models-step-09-mappings-tab.png)

Click **+ Add** and fill in:

* **Name\*** and **Description** — a label for this mapping
* **Models\*** — the model + SDK pairs this mapping allows
* **Scope\*** — **System**, **Workspace**, or **Project**
* **Default model** — required for System scope; optional for Workspace/Project (falls back to the next broader scope's default if unset)
* **Target Workspace(s)\*** / **Target Project(s)\*** — shown only for Workspace/Project scope; select one or more

![Add Model Mapping form](../../../.gitbook/assets/llm-models-step-10-add-mapping-empty.png)

![Add Model Mapping form filled in](../../../.gitbook/assets/llm-models-step-11-add-mapping-filled.png)

![New mapping added](../../../.gitbook/assets/llm-models-step-12-mapping-added.png)

{% hint style="info" %}
Resolution order is **Project → Workspace → System** — the most specific mapping that covers a given ticket wins. A fresh install seeds one **System**-scope mapping ("default models") automatically, so every workspace has a working default even before you add your own mappings.
{% endhint %}
