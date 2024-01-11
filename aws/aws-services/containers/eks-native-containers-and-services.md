---
description: Managing Containers and Service with EKS and Native Docker Services
---

# EKS/Native Containers and Services

{% hint style="info" %}
For an end-to-end example of creating an EKS Service, see [this tutorial](../../quick-start/quick-start-eks-services/).&#x20;

For a Native Docker Services example, see [this tutorial](../../quick-start/quick-start-duplocloud-docker-services/). &#x20;
{% endhint %}

## Services

Using the **Services** tab in the DuploCloud Portal (**DevOps** -> **Containers** -> **EKS** -> **Services**), you can display and manage the Services you have defined.

For EKS Services, select the Service **Name** and click the [**Actions** menu](eks-native-containers-and-services.md#7-toc-title-2) to **Edit** or **Delete** Services, in addition to performing other actions, as shown below.&#x20;

<figure><img src="../../../.gitbook/assets/sv_2.png" alt=""><figcaption><p><strong>Actions</strong> menu for EKS Service</p></figcaption></figure>

### Adding a DuploCloud EKS/Native Service

1. In the DuploCloud Portal, select **DevOps** -> **Containers** -> **EKS/Native** from the navigation pane.&#x20;
2. Click **Add**. The **Basic Options** section of the **Add Service** page displays.
3. Complete the fields on the page, including **Service Name**, **Docker Image** **name**, and number of **Replicas**. Use **Allocation Tags** to deploy the container in a specific set of hosts.&#x20;
4.  To force the creation of Kubernetes StatefulSets, select **Yes** in the **Force StatefulSets** field.\


    <div align="left">

    <img src="../../../.gitbook/assets/sv_1.png" alt="Add Service page">

    </div>
5. Click **Next.** The **Advanced Options** section of the **Add Service** page displays.
6. Configure advanced options as needed. For example, you can implement [Kubernetes Lifecycle Hooks](../../../kubernetes/kubernetes-lifecycle-hooks.md), by adding the YAML to the **Other Container Config** field (optional).&#x20;
7. Click **Create**. The Service is created.&#x20;

{% hint style="warning" %}
Do not use spaces when creating Service or Docker image names.

The number of Replicas you define must be less than or equal to the number of hosts in the fleet.
{% endhint %}

### Displaying Services <a href="#id-7-toc-title" id="id-7-toc-title"></a>

Once the deployment commands run successfully, click the **Services** tile on the **Tenants** page. Your deployments are displayed and you can now attach [load balancers](../load-balancers/) for the Services.

<figure><img src="../../../.gitbook/assets/sv_3 (1).png" alt=""><figcaption><p><strong>Tenants</strong> page with <strong>Services</strong> tile</p></figcaption></figure>

### Starting, stopping, and restarting multiple DuploCloud Services <a href="#id-7-toc-title" id="id-7-toc-title"></a>

Using the Services page, you can start, stop, and restart multiple services simultaneously.

1. In the DuploCloud Portal, navigate to **DevOps** -> **Containers** and select **EKS/Native** or **ECS**.&#x20;
2. Click the **Services** tab.&#x20;
3. Use the checkbox column to select multiple services you want to start or stop at once.
4. From the **Service Actions** menu, select **Start Service**, **Stop Service**, or **Restart Service.**

Your selected services are started, stopped, or restarted as you specified.

<figure><img src="../../../.gitbook/assets/image (117).png" alt=""><figcaption><p><strong>Services</strong> tab with checkbox column (highlighted) and <strong>Service Actions</strong> menu</p></figcaption></figure>

### Importing a Native Kubernetes Service <a href="#id-7-toc-title" id="id-7-toc-title"></a>

Using the **Import Kubernetes Deployment** pane, you can add a Service to an existing Kubernetes namespace using Kubernetes YAML.

1. In the DuploCloud Portal, select **DevOps** -> **Containers** -> **EKS/Native** from the navigation pane.&#x20;
2. Click **Add**. The **Add Service** page displays.
3. Click the **Import Kubernetes Deployment** button in the upper right. **The Import Kubernetes Deployment** pane displays.&#x20;
4. Paste the deployment YAML code, as in the example below, into the **Import Kubernetes Deployment** pane.&#x20;
5. Click **Import**.
6. In the **Add Service** page, click **Next.**
7. Click **Create**. Your Native Kubernetes Service is created.

<div align="left">

<figure><img src="../../../.gitbook/assets/image (116).png" alt=""><figcaption><p>YAML code for importing a Native Kubernetes Service</p></figcaption></figure>

</div>

{% code title="Sample YAML code" %}
```yaml
//apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: duploservices-my-tenant
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx1
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```
{% endcode %}

## Advanced configurations with EKS

You can supply advanced configuration options with EKS in the DuploCloud Portal in several ways, including the advanced use cases in this section.

### Enable DuploCloud Master IP access to an EKS Security Group

1. In the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Click the **System Config** tab.
3. Click **Add**. The **Add Config** pane displays.
4. From the **Config Type** list box, select, **Flags**.
5.  From the **Key** list box, select **Block Master VPC CIDR Allow in EKS SG**.\


    <div align="left">

    <figure><img src="../../../.gitbook/assets/image (114).png" alt=""><figcaption><p><strong>Add Config</strong> pane with <strong>Block Master VPC CIDR Allow in EKS SG</strong> setting</p></figcaption></figure>

    </div>


6. From the **Value** list box, select **True**.
7.  Click **Submit**. The setting is displayed as **BlockMasterVpcCidrAllowInEksSg** in the **System Config** tab.\


    <figure><img src="../../../.gitbook/assets/image (115).png" alt=""><figcaption><p><strong>System Config</strong> tab with <strong>Flag BlockMasterVpcCidrAllowInEksSg</strong> set to <strong>true</strong></p></figcaption></figure>

## Kubernetes Containers

Using the **Containers** tab in the DuploCloud Portal, you can display and manage the Containers you have defined.

Use the Options Menu ( <img src="../../../.gitbook/assets/Kabab_three_Vertical_dots (1).png" alt="" data-size="line"> ) in each Container row to display **Logs**, **State**, **Container Shell**, **Host Shell,** and **Delete** options.&#x20;

<table><thead><tr><th width="347">Option</th><th>Functionality</th></tr></thead><tbody><tr><td><strong>Logs</strong></td><td>Displays container logs. When you select this option, the Container Logs window displays. Use the <strong>Follow Logs</strong> option (enabled by default) to monitor logging in real-time for a running container. See the graphic below for an example of the Container Logs window.</td></tr><tr><td><strong>State</strong></td><td>Displays container state configuration, in YAML code, in a separate window.</td></tr><tr><td><strong>Container Shell</strong></td><td>Accesses the Container Shell. To access the <strong>Container Shell</strong> option, you must first set up <a href="../../prerequisites/kubectl-shell.md">Shell access for Docker</a>.</td></tr><tr><td><strong>Host Shell</strong></td><td>Accesses the Host Shell.</td></tr><tr><td><strong>Delete</strong></td><td>Deletes the container.</td></tr></tbody></table>

<div align="left">

<figure><img src="../../../.gitbook/assets/cont6.png" alt=""><figcaption><p><strong>Containers</strong> tab displaying defined containers with highlighted Options Menu</p></figcaption></figure>

</div>

### Downloading the Kubectl Token and KubeConfig <a href="#id-6-toc-title" id="id-6-toc-title"></a>

<div align="left">

<figure><img src="../../../.gitbook/assets/customlogs2.png" alt=""><figcaption><p><strong>Container Logs</strong> window with <strong>Follow Logs</strong> option enabled</p></figcaption></figure>

</div>

### Downloading the Kubectl Token and KubeConfig <a href="#id-6-toc-title" id="id-6-toc-title"></a>

DuploCloud provides you with a Just-In-Time (JIT) security token, for fifteen minutes, to access the `kubectl` cluster.&#x20;

1. In the DuploCloud Portal, select **Administrator**-> **Infrastructure** from the navigation pane.&#x20;
2. Select the Infrastructure in the **Name** column.
3. Click the **EKS** tab.&#x20;
4.  Copy the temporary **Token** and the **Server Endpoint** (Kubernetes URL) **Value**s from the Infrastructure that you created. You can also download the complete configuration by clicking the **Download Kube Config** button.\


    <figure><img src="../../../.gitbook/assets/k8s3.png" alt=""><figcaption><p><strong>EKS</strong> tab with <strong>Download KubeConfig</strong> button</p></figcaption></figure>


5. Run the following commands, in a local Bash shell instance:

```shell
> kubectl config --kubeconfig=config-demo set-cluster EKS_CLUSTER --server=[EKS_API_URL] --insecure-skip-tls-verify
```

```shell
> kubectl config --kubeconfig=config-demo set-credentials tempadmin --token=[TOKEN]
```

```shell
> kubectl config --kubeconfig=config-demo set-context EKS --cluster=EKS_CLUSTER --user=tempadmin --namespace=duploservices-[TENANTNAME]
```

```shell
> export KUBECONFIG=config-demo
```

```shell
> kubectl config use-context EKS
```

You have now configured `kubectl` to point and access the Kubernetes cluster. You can apply deployment templates by running the following command:

```shell
> kubectl apply -f nginx.yaml
```

{% code title="nginx.yaml" %}
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment-g
  labels:
    app: nginx-deployment-g
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx-deployment-g
  template:
    metadata:
      labels:
        app: nginx-deployment-g
    spec:
      nodeSelector:
        tenantname: "duploservices-stgeast1"
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```
{% endcode %}

If you need security tokens of a longer duration, create them on your own. Secure them outside of the DuploCloud environment.

### Passing Kubernetes Configs and Secrets

[See this section](../../../kubernetes/kubernetes-configs-and-secrets/) in the Duplocloud Kubernetes documentation.

### Downloading and configuring KubeCtl Token

[See this section](../../../kubernetes/kubectl-setup/kubernetes-kubectl-token.md) in the DuploCloud Kubernetes documentation.

### Setting Up Docker Registry Credentials

[See this section](docker-registry-credentials.md) in the DuploCloud documentation.

#### Add Pod Toleration spec to a Container configuration

See [Kubernetes Pod Toleration](../../../kubernetes/pod-toleration.md) for examples of specifying K8s YAML for Pod Toleration.
