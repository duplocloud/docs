---
description: Secret Management with DuploCloud, EVs, Kubernetes and Azure Key Vault
---

# Passing Configuration and Secrets

There are many ways to pass configuration to the containers at run time.

## **Environmental variables**

* This is the simplest way but can be cumbersome if there are too many configurations, especially files and certificates.
* In Kubernetes you also have the option to populate environment variables from [Config Maps](../../../aws/container-deployments/passing-config-and-secrets/setting-environment-variables-from-config.md#setting-environment-variables-from-a-kubernetes-configmap) or [Secrets](../../../aws/container-deployments/passing-config-and-secrets/setting-environment-variables-from-config.md#setting-environment-variables-from-a-kubernetes-secret).

## **Kubernetes**

### Config Maps

You can mount data from a Kubernetes Config Map [as files](../../../aws/container-deployments/passing-config-and-secrets/mounting-config-as-files.md#mount-a-kubernetes-configmap), or you can import it [as environment variables](../../../aws/container-deployments/passing-config-and-secrets/setting-environment-variables-from-config.md#setting-environment-variables-from-a-kubernetes-configmap).

### Secrets

You can mount data from a Kubernetes Secret [as files](../../../aws/container-deployments/passing-config-and-secrets/mounting-config-as-files.md#mount-a-kubernetes-secret), or you can import it [as environment variables](../../../aws/container-deployments/passing-config-and-secrets/setting-environment-variables-from-config.md#setting-environment-variables-from-a-kubernetes-secret).

## Azure Key Vault

DuploCloud Portal supports Azure Key Vault secret management. Navigate to **DevOps** -> **Keyvault** to add, store, and delete secrets.\
