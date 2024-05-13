---
description: Setting, mounting, and managing Kubernetes ConfigMaps and Kubernetes Secrets in DuploCloud environments.
---

# Kubernetes Configs and Secrets

In DuploCloud environments, you can pass configurations and Kubernetes [Secrets](https://kubernetes.io/docs/concepts/configuration/secret/) using Kubernetes [ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/) or through various strategies tailored to enhance security and management efficiency:

* **Setting Kubernetes Secrets directly in DuploCloud**: This involves creating secrets under Kubernetes > Secrets in the DuploCloud console. These secrets are then available in the Kubernetes environment and can be utilized as either files or environment variables. This method is straightforward, incurs no additional cost, and allows for the visibility of both secret keys and values within the DuploCloud console. For detailed instructions, see [Setting Kubernetes Secrets in DuploCloud](https://docs.duplocloud.com/docs/kubernetes-user-guide/configs-and-secrets/setting-kubernetes-secrets).

* **Settings Environment Variables (EVs) from a K8s ConfigMap or Secret**: This traditional method continues to be supported, offering a familiar approach to those accustomed to Kubernetes' native secrets management.

* **Mounting ConfigMaps and Secrets as files**: This method provides a seamless way to integrate configuration data directly into your application's file system.

Additionally, DuploCloud supports advanced secrets management strategies, including:

* **Using AWS as the Source of Truth**: By creating secrets in AWS Secrets Manager or Parameter Store and integrating them into Kubernetes secrets with SecretProviderClass, you benefit from advanced features like automatic rotation. This method displays only the secret keys in the DuploCloud console and involves a more complex setup but is ideal for centralizing secrets management across DuploCloud and non-DuploCloud resources. For more on this setup, visit [Adding SecretProviderClass Custom Resource in DuploCloud](https://docs.duplocloud.com/docs/kubernetes-user-guide/configs-and-secrets/adding-secretproviderclass-custom-resource#step-1-enable-secret-provider-class).

* **Application Directly Reads Secrets from AWS**: This approach allows the application code to directly fetch secrets from AWS Secret Manager or Parameter Store, managed via IAM roles facilitated by DuploCloud. It provides an added layer of protection and is particularly beneficial for development environments, though it requires modifications to the application code. Implementation guidance can be found in [AWS SDK for PHP - Managing Secrets](https://docs.aws.amazon.com/sdk-for-php/v3/developer-guide/secretsmanager-examples-manage-secret.html).

By leveraging these strategies, DuploCloud offers flexible and secure options for managing Kubernetes ConfigMaps and Secrets, catering to a variety of operational needs and security requirements.