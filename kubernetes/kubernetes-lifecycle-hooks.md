---
description: Implementing Kubernetes Lifecycle Hooks in DuploCloud
---

# Kubernetes Lifecycle Hooks

\
A [Kubernetes Lifecycle Hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) triggers events to run at different stages of a Container's lifecycle. These hooks run scripts or commands before or after a specific event, such as a container being created, started, or stopped. Lifecycle hooks perform tasks like starting services, or initializing, configuring, or verifying containers.

## Implementing Kubernetes Lifecycle Hooks

You can implement Kubernetes Lifecycle Hooks while [Adding a DuploCloud EKS/Native Service](../aws-user-guide/aws-services/containers/eks-containers-and-services.md#adding-a-duplocloud-eks-native-service) by adding the YAML like the example below to the **Other Container Config** field.&#x20;

```yaml
#lifecycle hook sample
lifecycle:
  postStart:
    exec:
      command:
        - /bin/sh
        - '-c'
        - date > /container-started.txt
  preStop:
    exec:
      command:
        - /usr/sbin/nginx
        - '-s'
        - quit
```

