---
description: Configuration and Secret management in Azure
---

# Passing Configs and Secrets

There are many ways to pass configurations to containers at run-time. Although simple to set up, using Environmental Variables can become complex if there are too many configurations, especially files and certificates. In Kubernetes, you also have the option to populate environment variables from [Config Maps](../../../kubernetes-overview/configs-and-secrets/mounting-config-as-files.md#creating-a-kubernetes-configmap) or [Secrets](../../../../kubernetes-overview/configs-and-secrets/setting-kubernetes-secrets.md#setting-kubernetes-secrets).

There are several methods for passing configurations to containers during runtime:.

1. **Environment Variables**: A simple method for passing configuration data, but it can become cumbersome when dealing with many configurations or sensitive data like certificates and keys.
2. **ConfigMaps and Secrets in Kubernetes**: For more structured management of configuration data, Kubernetes offers ConfigMaps for non-sensitive data and Secrets for sensitive data (e.g., passwords, tokens). These can be injected into containers at runtime, providing a cleaner and more secure way to manage configurations.
   * [Learn more about using ConfigMaps and Secrets in Kubernetes.](../../../kubernetes-overview/configs-and-secrets/)
3. **Azure Key Vault**: For Azure users, **Azure Key Vault** is an option to securely store and manage sensitive configurations and secrets outside of your application, reducing the complexity of handling sensitive data.
   * [Learn more about Azure Key Vault for secrets management.](../key-vault.md)
