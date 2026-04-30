# EKS Setup with Token

This guide walks through connecting an Amazon EKS cluster to DuploCloud using a Kubernetes service account token, then querying cluster data through the AI agent.

---

## Prerequisites — Generate a Service Account Token in EKS

Before configuring DuploCloud, create a dedicated service account in your EKS cluster with the permissions the AI agent needs.

### 1. Create the service account and RBAC resources

Save the following as `duplocloud-agent-rbac.yaml` and apply it to your cluster:

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

```bash
kubectl apply -f duplocloud-agent-rbac.yaml
```

### 2. Create a long-lived token secret (Kubernetes 1.24+)

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: duplocloud-agent-token
  namespace: kube-system
  annotations:
    kubernetes.io/service-account.name: duplocloud-agent
type: kubernetes.io/service-account-token
```

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

### 3. Extract the token

```bash
kubectl get secret duplocloud-agent-token -n kube-system \
  -o jsonpath='{.data.token}' | base64 --decode
```

Copy the output — you will paste it into DuploCloud in Step 3 below.

### 4. Get the cluster API endpoint

```bash
aws eks describe-cluster --name <your-cluster-name> \
  --query "cluster.endpoint" --output text
```

This returns a URL in the form `https://<id>.gr7.<region>.eks.amazonaws.com`. You will need this in Step 2.

---

## Step 1 — Navigate to Kubernetes Providers

Go to **AI Admin** → **Providers** → **IT**, then click the **Kubernetes** tab.

![Kubernetes providers list](../../.gitbook/assets/eks-step-02.png)

---

## Step 2 — Add an EKS Provider

Click **+ Add** and fill in the provider details:

- **Name** — a label for this cluster in DuploCloud
- **Type** — select **EKS**
- **API Endpoint** — the cluster endpoint URL from the prerequisite step above
- **Base64 Certificate Data** — optional; paste the cluster CA certificate if your cluster requires it

![Add EKS provider form](../../.gitbook/assets/eks-step-03.png)

Click **Create Provider**.

![Provider created successfully](../../.gitbook/assets/eks-step-04.png)

---

## Step 3 — Add a Kubernetes Token Credential

The new provider opens on the **Credentials** tab. Click **+ Add** and fill in:

- **Name** — a name for this credential
- **Authentication Type** — select **Kubernetes Token**
- **Token** — paste the service account token extracted in the prerequisite step

![Add Credential form with Kubernetes Token selected](../../.gitbook/assets/eks-step-06.png)

Click **Create**.

---

## Step 4 — Add a Scope

Switch to the **Scope** tab and click **+ Add**. Fill in:

- **Name** — a label for this scope
- **Credential** — select the token credential you just created
- **Namespace Regex** — use `*` to cover all namespaces, or restrict to a pattern (e.g. `production-.*`)
- **Namespaced Resource Types** — select **All Resources** to allow the agent to query any namespaced resource
- **Cluster Resource Types** — select **All Resources** to allow cluster-level queries (nodes, persistent volumes, etc.)

![Add Scope form — filled](../../.gitbook/assets/eks-step-07.png)

![Scope with resource types selected](../../.gitbook/assets/eks-step-08.png)

Click **Create**.

---

## Step 5 — Use EKS in a Ticket

Go to **AI DevOps** → **HelpDesk** → **Add Ticket**. Select **generic-agent** as the agent and choose your EKS scope from the scope dropdown.

![Selecting the EKS scope in a ticket](../../.gitbook/assets/eks-step-09.png)

Enter your request — for example, asking the agent to list nodes or check pod health.

![Ticket ready to submit](../../.gitbook/assets/eks-step-11.png)

Click **Create Ticket**. The agent connects to your EKS cluster using the token credential and returns the results.

![Agent response with EKS cluster data](../../.gitbook/assets/eks-step-12.png)
