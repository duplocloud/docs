# Containers

### Docker registry credentials <a href="#4-toc-title" id="4-toc-title"></a>

You can set Docker Credentials from  DevOps --> Containers --> AKS/Native --> **Docker Credentials**.

### Kubernetes Storage

User can configure StorageClass and PersistentVolumeClaims(PVC) from K8S Storage Tab. You can mount the StorageClass. Please find details [here](storage-options.md).

### Adding Service

&#x20;You can create Services from the portal, Implicitly, DuploCloud converts these services either into a Deployment Set or a StatefulSet. You can configure- images, the environment variable, map volumes, and mount volumes.

### Service Display

Once the deployment command runs successfully, go to the **Services** tab of the Tenant. You can see those deployments. You can also attach the load balancers for the services.

### Kubectl token and config

DuploCloud provides a way to connect to the Cluster namespace. You can follow the command, to access the cluster namespace. This option is available DevOps --> Containers --> AKS/Native --> Select KubeCtl Token

![](<../../../.gitbook/assets/image (1) (3).png>)

With these commands, you have configured the `kubectl` to access the kubernetes cluster for your tenant namespace.

