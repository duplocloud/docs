---
description: >-
  Connect a self-managed or on-premises Kubernetes cluster to DuploCloud AI by
  creating a service account token and registering it as a Kubernetes provider.
---

# Self-Managed / On-Prem Kubernetes

This guide is for clusters that DuploCloud does **not** provision for you — self-managed Kubernetes running on-premises, on bare metal, or on VMs (kubeadm, k3s, RKE, kubespray, and similar distributions).

For a managed cloud cluster, DuploCloud provides a turn-key integration that derives access from your cloud account — see [EKS](amazon-elastic-kubernetes-service-eks.md), [AKS](azure-kubernetes-service-aks.md), or [GKE](google-kubernetes-engine-gke.md). A self-managed cluster has no cloud IAM to delegate to, so you authenticate with a **Kubernetes service account token** that you create directly in the cluster and paste into DuploCloud.

The flow is:

1. Create a dedicated service account with RBAC scoped to the level of access your use cases require.
2. Mint a long-lived token for it and extract the token, the API endpoint, and the cluster CA certificate.
3. Register a **Kubernetes** provider of type **Other** in DuploCloud and add the token as a credential.

***

## Prerequisites

* `kubectl` access to the cluster with permission to create `ServiceAccount`, `ClusterRole`, `ClusterRoleBinding`, and `Secret` resources (cluster-admin or equivalent).
* Network reachability from where DuploCloud AI HelpDesk runs to the cluster's API server. On a private/on-prem cluster this is typically a LAN-routable address — it does not need to be internet-facing, but it must be reachable from the HelpDesk deployment.

***

## Step 1 — Create the service account and RBAC

Here is an example to start from — a service account with **read-only** access. Adjust the RBAC rules to match the level of access your use cases require (see the hint below), and update the `namespace` (`kube-system` in this example) to wherever you want the service account to live. Save the following as `duplocloud-agent-rbac.yaml`:

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: duplocloud-agent
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: duplocloud-agent-role
rules:
  - apiGroups: [""]
    resources:
      - nodes
      - pods
      - services
      - endpoints
      - namespaces
      - persistentvolumes
      - persistentvolumeclaims
      - events
      - configmaps
    verbs: ["get", "list", "watch"]
  - apiGroups: ["apps"]
    resources:
      - deployments
      - daemonsets
      - statefulsets
      - replicasets
    verbs: ["get", "list", "watch"]
  - apiGroups: ["batch"]
    resources: ["jobs", "cronjobs"]
    verbs: ["get", "list", "watch"]
  - apiGroups: ["metrics.k8s.io"]
    resources: ["nodes", "pods"]
    verbs: ["get", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: duplocloud-agent-binding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: duplocloud-agent-role
subjects:
  - kind: ServiceAccount
    name: duplocloud-agent
    namespace: kube-system
```

Apply it:

```bash
kubectl apply -f duplocloud-agent-rbac.yaml
```

{% hint style="info" %}
This grants **read-only** access — enough for the agent to query nodes, pods, deployments, events, and other resources. To let the agent take actions (scale, restart, apply), add the appropriate `verbs` (e.g. `update`, `patch`, `delete`, `create`) or bind to a broader ClusterRole such as `cluster-admin`. Grant only what your use case requires.
{% endhint %}

***

## Step 2 — Mint a long-lived token

On Kubernetes 1.24+, service accounts no longer auto-create a token secret. Create one explicitly — the cluster controller populates it with a non-expiring token and the cluster CA certificate:

```bash
kubectl apply -f - <<EOF
apiVersion: v1
kind: Secret
metadata:
  name: duplocloud-agent-token
  namespace: kube-system
  annotations:
    kubernetes.io/service-account.name: duplocloud-agent
type: kubernetes.io/service-account-token
EOF
```

***

## Step 3 — Extract the token, endpoint, and CA certificate

You need three values to register the provider.

**Token** — paste into the credential in Step 5:

```bash
kubectl get secret duplocloud-agent-token -n kube-system \
  -o jsonpath='{.data.token}' | base64 --decode
```

**API endpoint** — the cluster's API server URL, paste into the provider in Step 4:

```bash
kubectl config view --minify -o jsonpath='{.clusters[0].cluster.server}'
```

This returns a URL such as `https://k8s-api.internal.example.com:6443`.

**Cluster CA certificate (base64)** — paste into **Base64 Certificate Data** in Step 4. The token secret already holds it base64-encoded, so copy it as-is:

```bash
kubectl get secret duplocloud-agent-token -n kube-system \
  -o jsonpath='{.data.ca\.crt}'
```

{% hint style="warning" %}
For self-managed clusters the API server usually presents a **self-signed or private-CA** certificate. Supplying the CA certificate is what lets DuploCloud establish a trusted TLS connection — without it, the connection will fail certificate verification. This is the main difference from managed cloud clusters, where the CA is optional.
{% endhint %}

***

## Step 4 — Add the Kubernetes provider

In DuploCloud, go to **AI Admin** → **Providers** → **IT**, then open the **Kubernetes** tab and click **+ Add**. Fill in:

* **Name** — a label for this cluster in DuploCloud
* **Type** — select **Other** (the generic Kubernetes type, for clusters not managed through a cloud account)
* **API Endpoint** — the API server URL from Step 3
* **Base64 Certificate Data** — the base64 CA certificate from Step 3

Click **Create Provider**.

***

## Step 5 — Add the token credential

The new provider opens on the **Credentials** tab. Click **+ Add** and fill in:

* **Name** — a name for this credential
* **Authentication Type** — select **Kubernetes Token**
* **Token** — paste the decoded token from Step 3

Click **Create**.

***

## Step 6 — Add a scope

Switch to the **Scope** tab and click **+ Add**. Fill in:

* **Name** — a label for this scope
* **Credential** — select the token credential you just created
* **Namespace Regex** — use `*` to cover all namespaces, or restrict to a pattern (e.g. `production-.*`)
* **Namespaced Resource Types** — select **All Resources** to allow the agent to query any namespaced resource
* **Cluster Resource Types** — select **All Resources** to allow cluster-level queries (nodes, persistent volumes, etc.)

Click **Create**.
