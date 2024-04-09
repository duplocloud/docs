---
description: Kubernetes features in the DuploCloud Portal
coverY: 0
---

# Kubernetes Overview

DuploCloud leverages [Kubernetes](https://kubernetes.io/docs/home/) as a foundational building block behind many of its managed Services.&#x20;

As DuploCloud supports Kubernetes Cluster enablement on all public cloud platforms, there are many Kubernetes objects and components that you can work with. This includes handling high memory demands by identifying and reallocating resources as needed, such as moving a high-demand script to its own service with a `highmem` allocation tag for better performance.

Use the topics in this section to implement many Kubernetes features with little or no hard coding, using DuploCloud's no-code/low-code approach. This approach facilitates the autoscaling of an EKS cluster based on CPU/memory requests or limits, ensuring efficient resource utilization and optimal performance.

For information about public-cloud provider-specific Kubernetes container features, see the [Kubernetes Containers documentation](../aws-user-guide/aws-services/containers/eks-containers-and-services.md#kubernetes-containers) in AWS EKS, for example. Additionally, DuploCloud's integration with tools like Grafana and Prometheus allows for the setup of custom alerts for memory usage by pod, enhancing monitoring capabilities and operational visibility.

It's important to note that when managing Kubernetes clusters, the choice of instance types may depend on specific needs such as memory and CPU requirements. Therefore, selecting the appropriate instance type is crucial for balancing performance and cost.

Moreover, when adding an allocation group to an existing node with running services, it's essential to understand the implications for service continuity and whether a restart is necessary. This ensures that services remain available and performant during infrastructure changes.

In summary, DuploCloud provides a comprehensive suite of tools and features for managing Kubernetes clusters, from resource allocation and autoscaling to monitoring and alerting, all designed to support a wide range of use cases and performance requirements.