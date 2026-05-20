---
description: Kubernetes workloads — Deployments, DaemonSets, StatefulSets, and CronJobs running inside an Environment.
---

# Workloads

Workloads are the applications and services running inside your Kubernetes cluster. The AWS Extension supports the standard Kubernetes workload types: Deployments, DaemonSets, StatefulSets, and CronJobs.

## Spec

{% tabs %}
{% tab title="Deployment" %}
Runs a specified number of replica pods. Used for stateless applications and services.

| Field | Description |
|---|---|
| **Name** | The workload name |
| **Namespace** | The Namespace this workload runs inside |
| **Image** | The container image and tag |
| **Replicas** | Number of pod replicas |
| **Resource Requests and Limits** | CPU and memory allocation per pod |
| **Environment Variables** | Configuration passed to the container at runtime |
| **Secrets** | References to Kubernetes Secrets mounted as environment variables or volumes |
| **Volumes** | Persistent Volume Claims or ConfigMaps mounted into the container |
{% endtab %}

{% tab title="DaemonSet" %}
Runs one pod per node. Used for cluster-wide services like log collectors or monitoring agents.

| Field | Description |
|---|---|
| **Name** | The workload name |
| **Namespace** | The Namespace this workload runs inside |
| **Image** | The container image and tag |
| **Resource Requests and Limits** | CPU and memory allocation per pod |
| **Environment Variables** | Configuration passed to the container at runtime |
| **Secrets** | References to Kubernetes Secrets mounted as environment variables or volumes |
| **Volumes** | Persistent Volume Claims or ConfigMaps mounted into the container |
{% endtab %}

{% tab title="StatefulSet" %}
Runs pods with stable network identities and persistent storage. Used for stateful applications like databases and message queues.

| Field | Description |
|---|---|
| **Name** | The workload name |
| **Namespace** | The Namespace this workload runs inside |
| **Image** | The container image and tag |
| **Replicas** | Number of pod replicas |
| **Resource Requests and Limits** | CPU and memory allocation per pod |
| **Environment Variables** | Configuration passed to the container at runtime |
| **Secrets** | References to Kubernetes Secrets mounted as environment variables or volumes |
| **Volumes** | Persistent Volume Claims providing stable, pod-specific storage |
{% endtab %}

{% tab title="CronJob" %}
Runs jobs on a scheduled basis. Each run creates a short-lived Job pod that completes and terminates.

| Field | Description |
|---|---|
| **Name** | The workload name |
| **Namespace** | The Namespace this workload runs inside |
| **Image** | The container image and tag |
| **Resource Requests and Limits** | CPU and memory allocation per pod |
| **Environment Variables** | Configuration passed to the container at runtime |
| **Secrets** | References to Kubernetes Secrets mounted as environment variables or volumes |
{% endtab %}
{% endtabs %}

## Dependencies

Workloads require an **Environment** and a **Namespace**.
