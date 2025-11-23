# View Presidio Details

## Duplo Presidio

The **Duplo Presidio Service** is a wrapper built on top of [Microsoft Presidio](https://microsoft.github.io/presidio/) that enhances its ability to detect and protect sensitive data by supporting **custom recognizers and anonymizers**.

This ensures that secrets, tokens, passwords, and credentials are automatically identified and anonymized before data leaves your Duplo-managed Kubernetes cluster. By disabling irrelevant recognizers and introducing project-specific patterns, we reduce noise and improve accuracy.

### 📂 Structure of the ConfigMap

Presidio is configured through a **YAML-based ConfigMap**.\
This config controls global flags, disabled built-in recognizers, and custom recognizers that we add.

Example (simplified from our deployment):

```
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
```

### 🔎 Built-in Recognizers

Presidio ships with a rich set of **built-in recognizers** for detecting common forms of sensitive data (PII). These recognizers are enabled by default and cover global as well as region-specific entities.

👉 See the full list of built-in recognizers here:\
[Presidio Supported Entities](https://microsoft.github.io/presidio/supported_entities/)

#### Examples of Built-in Recognizers

* **EmailRecognizer** → detects email addresses
* **PhoneRecognizer** → phone numbers
* **UrlRecognizer** → web URLs
* **IpRecognizer** → IPv4/IPv6 addresses
* **CreditCardRecognizer** → credit card numbers
* **UsSsnRecognizer** → U.S. Social Security Numbers
* **PersonRecognizer** → human names
* **IbanRecognizer** → IBAN bank account numbers<br>

### ✂️ Built-in Anonymizers

While **recognizers** detect sensitive data, **anonymizers** transform or redact that data to protect it. Presidio comes with several built-in anonymizers that can be applied when sanitizing text.

#### Common Anonymizers

* **replace** → Replaces detected entity with a placeholder (e.g., `<ENTITY_TYPE>`)
* **mask** → Masks characters with a symbol (e.g., `****1234`)
* **redact** → Removes the detected entity entirely
* **hash** → Hashes the entity value (SHA256 by default)
* **encrypt / decrypt** → Encrypts or decrypts values using AES

👉 Full list of built-in anonymizers:\
[Presidio Anonymizers Documentation](https://microsoft.github.io/presidio/anonymizer/anonymizers/)
