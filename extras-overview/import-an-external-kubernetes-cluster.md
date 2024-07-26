# Import an External Kubernetes Cluster

DuploCloud allows an external or an On-Premises Kubernetes Cluster to be imported as an Infrastructure that is managed by the Platform.

### Prerequisite

The Kubernetes Cluster that needs to be importaed should be ready to use and accessible using kubectl shell.

## Import External K8s Cluster with Admin permission

### 1. Creating a service account in K8s cluster with admin setup

1. Save the below content as a file name **service-account-admin-setup.yaml**

```yaml
example with admin access
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: duplo-admin-user
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: duplo-admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: duplo-admin-user
  namespace: kube-system
---
apiVersion: v1
kind: Secret
metadata:
  name: duplo-admin-token
  namespace: kube-system
  annotations:
    kubernetes.io/service-account.name: duplo-admin-user
type: kubernetes.io/service-account-token
---
```

2. Run `kubectl apply -f service-account-admin-setup.yaml`. This will create a new service account with admin permission.
3. Run `kubectl -n kube-system describe secret duplo-admin-token` to fetch the token to use in DuploCloud to import the cluster.

### 2. Import the Kubernetes cluster in DuploCloud

{% hint style="warning" %}
Before performing this step, Contact DuploCloud Support to enable the configuration that allows import of an external Kubernetes cluster.
{% endhint %}

1. Go to DuploCloud portal **Administrator --> Infrastructure** page and click Add.
2. From **Cloud** dropdown, select **On-Premises.**
3. Enter all the details of the Kubernetes Cluster&#x20;
   * Kubernetes Cluster Name
   * Kubernetes Cluster Endpoint
   * Kubernetes Token got from Step 1.3.
   * Kubernetes Cluster Certificate Authority Data (For EKS cluster this can be fetched from EKS Cluster overview page from AWS Console).&#x20;
   * Kubernetes Vendor as EKS (as shown in the example below)

<figure><img src="../.gitbook/assets/image (163).png" alt=""><figcaption></figcaption></figure>

### 3. View Imported Kubernetes Cluster from DuploCloud

<figure><img src="../.gitbook/assets/image (164).png" alt=""><figcaption></figcaption></figure>

### 4. Adding Existing Nodes for the imported cluster in DuploCloud Portal

1. Create a Tenant for the Infrastructure created in above steps.
2. Click on On-Premises Tab and click on Add

<figure><img src="../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>

3. You can import existing nodes

<figure><img src="../.gitbook/assets/image (166).png" alt=""><figcaption></figcaption></figure>

4. View imported Nodes.

<figure><img src="../.gitbook/assets/image (167).png" alt=""><figcaption></figcaption></figure>

### 5. Creating a WebServer Service with Cloud as On-Prem

You can create a Service by selecting **Cloud** as **OnPrem.**

<figure><img src="../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure>

Once service is created, you should be able to access KubeCtl shell, retrieve KubeToken, Host/ Container shell, Container logs for the service created.

<figure><img src="../.gitbook/assets/image (170).png" alt=""><figcaption></figcaption></figure>

## Import External Kubernetes Cluster as Read-Only

Administrator can import external Kubernetes cluster in DuploCloud Portal with Read Only access.

### 1. Creating a service account in K8s cluster with **readonly** user

1. Save the below content as a file name **service-account-readonly-setup.yaml**

```yaml
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: duplo-readonly-user
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: duplo-readonly-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: view
subjects:
- kind: ServiceAccount
  name: duplo-readonly-user
  namespace: kube-system
---
apiVersion: v1
kind: Secret
metadata:
  name: duplo-readonly-token
  namespace: kube-system
  annotations:
    kubernetes.io/service-account.name: duplo-readonly-user
type: kubernetes.io/service-account-token
---
```

2. Run `kubectl apply -f service-account-readonly-setup.yaml`. This will create a new service account with readonly permission.
3. Run `kubectl -n kube-system describe secret duplo-readonly-token` to fetch the token to use in DuploCloud to import the cluster.

### 2. Import the Kubernetes cluster in DuploCloud.&#x20;

Follow this step to [import](import-an-external-kubernetes-cluster.md#id-2.-import-the-kubernetes-cluster-in-duplocloud) and [view](import-an-external-kubernetes-cluster.md#view-imported-kubernetes-cluster-from-duplocloud) the cluster.

User will only be able to view the Kubernetes resources. You will not be able to add Nodes, create or update any services in Read Only mode.

\
