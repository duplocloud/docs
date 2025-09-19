# View Presidio Details

The **Duplo Presidio Service** is a wrapper built on top of [Microsoft Presidio](https://microsoft.github.io/presidio/) that enhances its ability to detect and protect sensitive data by supporting **custom recognizers and anonymizers**.  

This ensures that secrets, tokens, passwords, and credentials are automatically identified and anonymized before data leaves your Duplo-managed Kubernetes cluster. By disabling irrelevant recognizers and introducing project-specific patterns, we reduce noise and improve accuracy.

---

## 📂 Structure of the ConfigMap

Presidio is configured through a **YAML-based ConfigMap**.  
This config controls global flags, disabled built-in recognizers, and custom recognizers that we add.

Example (simplified from our deployment):

```yaml
config: |
  global_regex_flags: 26
  supported_languages:
    - en

  # Disable unnecessary built-in recognizers
  disabled_recognizers:
    - DateRecognizer
    - UrlRecognizer
    - DomainRecognizer
    - EmailRecognizer
    - PersonRecognizer
    - LocationRecognizer

  # Example custom recognizers
  recognizers:
    - name: GitHubTokenRecognizer
      type: custom
      supported_entity: GITHUB_TOKEN
      patterns:
        - name: github_token_pattern
          regex: \b(ghp_[0-9a-zA-Z]{36})\b
          score: 0.95

    - name: PrivateKeyRecognizer
      type: custom
      supported_entity: PRIVATE_KEY
      patterns:
        - name: rsa_private_key_pattern
          regex: -----BEGIN\s+(?:RSA\s+)?PRIVATE\s+KEY-----[\s\S]*?-----END\s+(?:RSA\s+)?PRIVATE\s+KEY-----
          score: 0.99
