---
description: ConfigMaps and Kubernetes Secrets for managing configuration and sensitive data.
---

# Configs and Secrets

**ConfigMaps** store non-sensitive configuration data — feature flags, connection strings, application settings — as key-value pairs that workloads can consume as environment variables or mounted files.

**Secrets** store sensitive data such as passwords, API keys, and TLS certificates. Secrets are base64-encoded in Kubernetes and can be consumed by workloads in the same way as ConfigMaps.

## ConfigMaps

| Field | Description |
|---|---|
| **Name** | The ConfigMap name |
| **Namespace** | The Namespace this ConfigMap belongs to |
| **Data** | Key-value pairs of configuration data |

## Secrets

| Field | Description |
|---|---|
| **Name** | The Secret name |
| **Namespace** | The Namespace this Secret belongs to |
| **Type** | The Secret type (e.g. `Opaque`, `kubernetes.io/tls`) |
| **Data** | Key-value pairs of sensitive data |

## Dependencies

ConfigMaps and Secrets require an **Environment** and a **Namespace**.
