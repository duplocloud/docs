# GCP Vertex AI Support

An Agent SDK can run against GCP Vertex AI as its model backend, alongside the existing AWS Bedrock, Azure AI Foundry, and direct Anthropic API options.

As with the other provider options, this is configured on the Agent SDK's own deployment rather than in AI Admin — see [LLM Models](llm-models.md) for how provider selection works generally. To route an Agent SDK through Vertex AI, set on its container:

* **`CLOUD_PROVIDER=GCP`**
* **`GOOGLE_CLOUD_PROJECT`** — the GCP project ID Vertex AI calls are billed/scoped to
* **`CLOUD_ML_REGION`** (optional) — defaults to `global` if unset

The preferred authentication method is **Workload Identity Federation** on GKE, which avoids managing a long-lived API key: the GKE service account needs Workload Identity enabled and an IAM binding granting it Vertex AI access.

{% hint style="info" %}
Requests made through this path are automatically tagged with DuploCloud's GCP partner attribution, identifying them as originating through DuploCloud's integration — this happens transparently and needs no configuration.
{% endhint %}

If an Agent SDK's deployment also has `ANTHROPIC_API_KEY` or Azure Foundry variables set, those take priority — Vertex AI is only used when neither of those is configured and `CLOUD_PROVIDER=GCP` is set. With none of these set, an Agent SDK falls back to AWS Bedrock by default.
