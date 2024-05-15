---
description: Manage and troubleshooting services with HPA configured.
---

# HPA

## Using the Horizontal Pod Autoscalar (HPA) in AWS

See the [Autoscaling in Kubernetes](../overview/use-cases/hosts-vms/auto-scaling/kubernetes-scaling-options.md) topic in the AWS DuploCloud documentation.

## Managing Services with HPA

When working with Kubernetes services configured with Horizontal Pod Autoscaler (HPA), it's important to understand how to manage and troubleshoot them effectively.

### Stopping a Service with HPA

To stop a service that is hung in a Running state due to HPA, you cannot directly delete pods, as new ones are created to maintain the set number of replicas. Instead, remove the HPA configuration and adopt a static replication strategy by setting the replica count to 0. This ensures the service is effectively stopped without attempting to set `minReplicas` to 0, which is an invalid configuration for HPA.

### Troubleshooting

If issues arise while stopping a service with HPA configured, avoid setting `minReplicas` it to 0 and ensure the HPA configuration is removed in favor of a static replication strategy. For further troubleshooting, consult the Faults menu under the DevOps section in the DuploCloud UI, where all errors are logged, facilitating efficient diagnosis and resolution.

### UI Improvements

DuploCloud is planning enhancements to the UI to improve the management of services running with HPA configurations. These improvements include adding validation to prevent set `minReplicas` to 0, potentially removing the `Stop` option for services with HPA, and clearly documenting the correct procedure for stopping such services. These updates aim to simplify the process and prevent common configuration mistakes, ensuring a smoother experience in managing Kubernetes services with HPA.
