---
description: Kubernetes features in the DuploCloud Portal
coverY: 0
---

# Kubernetes Overview

DuploCloud leverages [Kubernetes](https://kubernetes.io/docs/home/) as a foundational building block behind many of its managed Services.&#x20;

As DuploCloud supports Kubernetes Cluster enablement on all public cloud platforms, there are many Kubernetes objects and components that you can work with. This includes handling high memory demand issues effectively, as demonstrated by the resolution of an eventarchiver pod requiring 30GB of memory. By moving the script to its own service and allocating it to a larger instance with a 64GB limit and a `highmem` allocation tag, DuploCloud showcases its capability to manage resources efficiently.

Use the topics in this section to implement many Kubernetes features with little or no hard coding, using DuploCloud's no-code/low-code approach. This approach extends to configuring cluster autoscaling based on CPU/memory requests or limits, ensuring that your EKS cluster scales appropriately to meet demand.

For information about public-cloud provider-specific Kubernetes container features, see the [Kubernetes Containers documentation](../aws-user-guide/aws-services/containers/eks-containers-and-services.md#kubernetes-containers) in AWS EKS, for example. It's important to note that the choice of instance types for Kubernetes in DuploCloud is flexible, catering to specific needs such as memory and CPU requirements.

Additionally, DuploCloud's integration with monitoring tools like Grafana and Prometheus allows for the setup of custom alerts for memory usage by pod, enhancing the observability of your Kubernetes environment. This capability ensures that you can maintain optimal performance and resource utilization across your clusters.

Understanding the implications of operational actions, such as adding an allocation group to an existing node with running services, is crucial for service continuity. While the document does not explicitly detail the behavior in this scenario, it underscores the importance of considering the impact on running services, whether they require a restart or can automatically move to another instance.

In summary, DuploCloud's Kubernetes support encompasses a broad range of functionalities from resource management and autoscaling to advanced monitoring, all designed to simplify Kubernetes operations for users across all public cloud platforms.