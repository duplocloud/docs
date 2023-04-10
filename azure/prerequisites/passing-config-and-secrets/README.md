---
description: Set up secret management using EVs, Kubernetes, and Azure Key Vault
---

# Set up config and secret management

There are numerous ways to pass configurations to containers at run time. As you set up your Azure DuploCloud environment, consider the following options for configuration and secret management.

## **Environmental variables (EVs)**

* Using EVs can be a simple method for configuration and secret management, but can be more complex if you have many configurations, especially for files and certificates.
* In Kubernetes, you have the option to populate environment variables from [Config Maps](../../../aws/use-cases/passing-secrets/passing-config-and-secrets/setting-environment-variables-from-config.md#setting-environment-variables-from-a-kubernetes-configmap) or [Secrets](../../../aws/use-cases/passing-secrets/passing-config-and-secrets/setting-environment-variables-from-config.md#setting-environment-variables-from-a-kubernetes-secret).

## **Kubernetes**

### Config Maps

You can mount data from a Kubernetes ConfigMap [as files](../../../aws/use-cases/passing-secrets/passing-config-and-secrets/mounting-config-as-files.md#mount-a-kubernetes-configmap) or import it [as environment variables](../../../aws/use-cases/passing-secrets/passing-config-and-secrets/setting-environment-variables-from-config.md#setting-environment-variables-from-a-kubernetes-configmap).

### Secrets

You can mount data from a Kubernetes Secret [as files](../../../aws/use-cases/passing-secrets/passing-config-and-secrets/mounting-config-as-files.md#mount-a-kubernetes-secret) or import it [as environment variables](../../../aws/use-cases/passing-secrets/passing-config-and-secrets/setting-environment-variables-from-config.md#setting-environment-variables-from-a-kubernetes-secret).

## Azure Key Vault

DuploCloud Portal supports Azure Key Vault for secrets management.&#x20;

In the Portal, navigate to **DevOps** -> **Keyvault** to add, store, and delete secrets.\
