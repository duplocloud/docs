---
description: At Rest encryption support in DuploCloud
---

# At Rest Encryption

DuploCloud automatically encrypts resources at rest using cloud provider–specific keys. This ensures that all data stored in cloud resources is protected by default.

When creating resources, encryption is applied using one of the following options:

1. **Default Tenant Key** – A key automatically generated and managed by the cloud provider for the Tenant. This key is applied by default if no custom key is available.
2. **Plan-level custom KMS key** – A custom key added to a Plan. This key can be used for resources across all Tenants in the Plan.
3. **Tenant-level custom KMS key** – A custom key added to a specific Tenant. This key can only be used for resources created within that Tenant.

These options give users flexibility to apply encryption strategies that meet their specific requirements.

{% hint style="info" %}
For detailed instructions on adding Plan-level or Tenant-level keys and selecting them when creating resources, see the [KMS Keys documentation](at-rest-encryption/kms-keys.md).
{% endhint %}

