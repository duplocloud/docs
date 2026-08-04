# Direct Anthropic API Support

An Agent SDK can call the Anthropic API directly, instead of routing through AWS Bedrock, GCP Vertex AI, or Azure AI Foundry.

This isn't something you turn on in the app — as noted in [LLM Models](llm-models.md), which underlying provider an Agent SDK actually runs on is determined by environment variables on that Agent SDK's own deployment, not by any setting in AI Admin. To use the Anthropic API directly, set an `ANTHROPIC_API_KEY` on the Agent SDK's container. No other provider-related variable is needed.

{% hint style="info" %}
Provider selection is per-Agent-SDK, not a single platform-wide switch. Since every registered Agent SDK is its own deployed service, different Agent SDKs in the same portal can run against different providers at the same time — one calling Anthropic directly while another runs on Bedrock, for example.
{% endhint %}

If an Agent SDK's deployment has more than one provider's variables set, `ANTHROPIC_API_KEY` takes priority over GCP Vertex AI or Azure Foundry configuration — direct Anthropic API access wins whenever a key is present.
