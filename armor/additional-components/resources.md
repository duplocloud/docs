# Resources

The Resources section gives you a unified view of infrastructure resources managed across your cloud providers. From the left navigation sidebar, expand **Resources** to access provider sub-sections.

When a cloud **Provider** is configured, its resources are automatically discovered and displayed here. For example, DuploCloud AI Suite supports viewing AWS resources (EC2, RDS, S3, and more) and Kubernetes resources (Pods, Deployments, Services, and more).

---

## AWS Resources

Selecting **AWS** under Resources opens the AWS resource browser, displaying resources from the currently selected scope.

### EC2 Instances

The default view shows **EC2 Instances** — virtual machines running in your cloud environment. The table displays each instance's name, instance ID, type, state, availability zone, private and public IP addresses, and VPC.

![EC2 Instances overview](../../../../.gitbook/assets/resources-step-01-aws-ec2.png)

---

### Switching Scopes

The **Scope** selector at the top right of the page shows the current cloud account and tenant being viewed. Click it to open a dropdown listing all available scopes you have access to.

![Scope selector](../../../.gitbook/assets/resources-step-02-scope-selector.png)

![Scope dropdown open](../../../.gitbook/assets/resources-step-03-scope-open.png)

Select a different scope to view resources in that environment. The table immediately updates to show resources belonging to the selected scope.

![Scope selected](../../../.gitbook/assets/resources-step-04-scope-sandbox.png)

---

### RDS Databases

Click the **RDS DBInstance** tab to view managed relational database instances. The table shows each database's name, role, engine type, endpoint, status, and instance size.

![RDS DBInstance tab](../../../.gitbook/assets/resources-step-05-aws-rds.png)

---

### S3 Buckets

Click the **S3 Bucket** tab to view object storage buckets. The table shows each bucket's name and ARN.

![S3 Bucket tab](../../../.gitbook/assets/resources-step-06-aws-s3.png)

---

## Kubernetes Resources

Selecting **Kubernetes** under Resources opens the Kubernetes resource browser. The tab bar at the top lets you switch between resource types: Pods, Deployments, DaemonSets, StatefulSets, Jobs, CronJobs, Services, and more.

### Pods

The default Kubernetes view shows **Pods** — the basic unit of deployment in Kubernetes. The table displays each pod's name, namespace, containers, restart count, controlling resource, node, QoS class, and status.

![Kubernetes Pods overview](../../../.gitbook/assets/resources-step-07-k8s-pods.png)

---

### Switching Scope and Namespace

The Kubernetes resource view provides two selectors in the page header:

- **Scope** — selects the Kubernetes cluster or environment to inspect
- **Namespace** — filters resources to a specific Kubernetes namespace within that scope

#### Changing the Scope

Click the **Scope** badge in the header to open the scope dropdown, which lists all Kubernetes clusters you have access to.

![K8s scope selector](../../../.gitbook/assets/resources-step-08-k8s-scope-selector.png)

![K8s scope dropdown](../../../.gitbook/assets/resources-step-09-k8s-scope-open.png)

Select the desired scope. The resource list updates immediately to show resources in the selected cluster.

![Scope selected](../../../.gitbook/assets/resources-step-09b-k8s-scope-selected.png)

#### Changing the Namespace

Click the **Namespace** badge next to the scope to open the namespace dropdown, which lists all namespaces available within the current scope.

![K8s namespace selector](../../../.gitbook/assets/resources-step-10-k8s-namespace-selector.png)

![K8s namespace dropdown](../../../.gitbook/assets/resources-step-11-k8s-namespace-open.png)

Select a namespace to filter the displayed resources.

---

### Deployments

Click the **Deployments** tab to view Kubernetes Deployments. The table shows each deployment's name, namespace, pod count, replica count, status, and age.

![Kubernetes Deployments](../../../.gitbook/assets/resources-step-12-k8s-deployments.png)

---

### Services

Click the **Services** tab to view Kubernetes Services. The table shows each service's name, namespace, type, cluster IP, ports, external IP, status, and age.

![Kubernetes Services](../../../.gitbook/assets/resources-step-13-k8s-services.png)
