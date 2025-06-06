---
description: Import an external or On-Prem cluster to be managed by DuploCloud
---

# Import an External Kubernetes Cluster

DuploCloud allows an external or an On-Premises Kubernetes (K8s) Cluster to be imported as an Infrastructure that the DuploCloud Platform manages.

## Prerequisite

The Kubernetes Cluster that needs to be imported should be ready to use and accessible using the `kubectl`shell.

## Creating a service account in the K8s cluster with admin permissions

1. Save this YAML code as a file name **service-account-admin-setup.yaml**.

{% code title="service-account-admin-setup.yaml" %}
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
{% endcode %}

2. Run `kubectl apply -f service-account-admin-setup.yaml`, creating a new service account with Administrator permissions.
3. Run `kubectl -n kube-system describe secret duplo-admin-token` to fetch the token for DuploCloud to use when importing the cluster.

## Importing your Kubernetes Cluster to DuploCloud

{% hint style="warning" %}
Before performing this step, Contact DuploCloud Support to enable the configuration that allows the import of an external Kubernetes cluster.
{% endhint %}

1. In the DuploCloud Portal, navigate to **Administrator -> Infrastructure**.
2. Click **Add**. The **Add Infrastructure** page displays.
3. From the **Cloud** list box, select **On-Premises**.
4. Enter the details of the Kubernetes Cluster:&#x20;
   * Kubernetes Cluster **Name**
   * **Kubernetes Cluster Endpoint**
   * **Kubernetes** Token, which you retrieved when you [created a service account in the previous step](import-an-external-kubernetes-cluster.md#creating-a-service-account-in-the-k8s-cluster-with-admin-permissions).
   * **Kubernetes Cluster Certificate Authority Data** (For an EKS cluster, this can be copied from the **EKS Cluster Overview** page from the AWS Console).&#x20;
   * **Kubernetes Vendor** (Enter **EKS**, as in the example below).

<figure><img src="../.gitbook/assets/image (421).png" alt=""><figcaption><p><strong>Add Infrastructure</strong> page</p></figcaption></figure>

## Viewing Imported Kubernetes Cluster from DuploCloud

Select the **Kubernetes** tab to display information about the imported Kubernetes Cluster.

<figure><img src="../.gitbook/assets/image (422).png" alt=""><figcaption><p>The <strong>Kubernetes</strong> tab</p></figcaption></figure>

## Adding Existing Nodes for the imported cluster in DuploCloud&#x20;

1. Select the Tenant from the **Tenant** list box.&#x20;
2. Navigate to **Kubernetes** -> **Nodes**. The **Nodes** page displays.
3. Click the **On-Premises** Tab.
4. Click **Add**. The **Add On-Premesis** Instance pane displays.
5. Select the node from the **Kubernetes Node** list box.&#x20;
6. Supply an **Allocation Tag**.
7.  Click **Add**.\


    <div align="left"><figure><img src="../.gitbook/assets/image (6) (3).png" alt="" width="381"><figcaption><p>The <strong>Add On-Premises Instance</strong> pane</p></figcaption></figure></div>

## Creating a WebServer Service with Cloud as On-Premises

Create a WebServer Service in the DuploCloud portal by selecting **OnPrem** from the **Cloud** list box while creating a [Kubernetes Service](../welcome-to-duplocloud/application-focussed-interface/duplocloud-common-components/app-service-and-cloud-services.md).

<figure><img src="../.gitbook/assets/image (426).png" alt=""><figcaption><p>The <strong>Basic Options</strong> page to add a Kubernetes Service with the <strong>Cloud</strong> list box set to <strong>OnPrem</strong></p></figcaption></figure>

Once the service is created, you should be able to access the [`kubectl` shell](kubectl/kubectl-shell/#accessing-the-kubectl-shell-in-the-duplocloud-portal), retrieve the [KubeCtl Token](kubectl-setup/kubectl-token.md), [Host/Container shell, and Container logs](../overview/aws-services/containers/eks-containers-and-services/#kubernetes-containers) for the service you created.

<figure><img src="../.gitbook/assets/image (428).png" alt=""><figcaption><p><strong>Containers</strong> tab for a Kubernetes Service</p></figcaption></figure>

## Importing External Kubernetes Cluster as Read-Only

An administrator can import an external Kubernetes cluster in the DuploCloud Portal with `readonly` access.

### Creating a Service Account in the K8s cluster with R**ead-Only** Access

1. Save the following YAML code as **service-account-readonly-setup.yaml**.

{% code title="service-account-readonly-setup.yaml" %}
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
{% endcode %}

2. Run `kubectl apply -f service-account-readonly-setup.yaml`, creating a new service account with `readonly` permission.
3. Run `kubectl -n kube-system describe secret duplo-readonly-token` to fetch the token for DuploCloud to use when importing the cluster.

### Importing the Kubernetes cluster to DuploCloud&#x20;

Follow this step to [import](import-an-external-kubernetes-cluster.md#importing-your-kubernetes-cluster-to-duplocloud) and [view](import-an-external-kubernetes-cluster.md#viewing-imported-kubernetes-cluster-from-duplocloud) the cluster.

{% hint style="warning" %}
DuploCloud users with non-administrator access (**User** role) can only view Kubernetes resources. They cannot add Nodes or create or update any Services in `readonly` mode.\

{% endhint %}
