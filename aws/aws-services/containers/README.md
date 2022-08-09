# Containers

## Docker native <a href="#0-toc-title" id="0-toc-title"></a>

Any docker container can be deployed in the VM. Go to **DevOps** > **Containers** > **EKS/Native** > **+Add** button above the table. Give a name for your services (no spaces); number of replicas; Docker image; volumes (if any). The number of replicas must be less than or equal to the number of hosts in the fleet. You can use `AllocationTags` to deploy the container in a specific set of hosts.\


![](<../../../.gitbook/assets/image (13) (1) (1).png>)

## Kubernetes cluster <a href="#1-toc-title" id="1-toc-title"></a>

DuploCloud supports EKS and AKS out of box. Kubernetes clusters are created during Infrastructure setup under **Administrator > Infrastructure**. The cluster is created in the same VPC as the Infrastructure. Typically, it takes 10 minutes for an Infrastructure with AKS/EKS cluster to be ready. Next, we will walk you through deploying an application within a Tenant in Kubernetes. The application will comprise of set of VMs, Deploymentset (pods) with an application load balancer. Pods can be deployed either through the DuploCloud Portal or through Kubectl (HelmCharts)

## Adding tenants <a href="#2-toc-title" id="2-toc-title"></a>

We map each tenant to a namespace in Kubernetes. For example, if a tenant is called analytics in DuploCloud, then there will be a namespace called duploservices-analytics in Kubernetes. All components of an application within this tenant are placed in this namespace. Since Nodes cannot be part of namespace in Kubernetes, we set a label called “`tenantname`” for all the nodes that are launched within the tenant. For example, a node launched in the analytics tenant will have label called “`tenantname: duploservices-analytics`“. Any pods that are launched through the DuploCloud UI will have appropriate nodeselector to tie the pod to the nodes within the tenant. If you are deploying directly via kubectl then make sure your deployment has the appropriate nodeselector.

## Adding hosts <a href="#3-toc-title" id="3-toc-title"></a>

Once the tenant is created. You can go to **DevOps** and change to the particular tenant. Under the hosts menu, start by creating new Nodes (Hosts). Make sure the value of pool is set to “Eks Linux” (which will be the default).

## Docker registry credentials and Kubernetes secrets <a href="#4-toc-title" id="4-toc-title"></a>

These can be set **DevOps** > **Containers** > **EKS/Native** tabs. Docker registry credentials are passed to the Kubernetes cluster as `kubernetes.io/dockerconfigjson`. Other Kubernetes secrets can also be set here and referenced in your deployment later.

## Adding services <a href="#5-toc-title" id="5-toc-title"></a>

When we say services, we don’t mean a Kubernetes service, but we mean the DuploCloud term service (See terminology at the top). You can deploy DuploCloud services by clicking **+Add** button under the **EKS/Native** tab. Implicitly, DuploCloud converts these services either into a deployment set or a stateful set. If there are no volume mappings, then it is a deployment set, otherwise it is a stateful set. Most configs are self-explanatory, for example, Images, Replicas and environmental variables.

The other advanced configuration can be provided under the other K8 Config section. The content of this section is a one-to-one mapping of the Kubernetes API. All types of configurations for deployments are stateful sets and are supported, while putting the appropriate JSON under the other K8 Config section. For example, to reference the secrets via config map, the JSON would look like the following:

```json
{
	"Volumes": [
		{
			"name": "config-volume",
			"configMap": {
				"name": "game-config"
			}
		}
	],
	"VolumesMounts": [
		{
			"name": "config-volume",
			"mountPath": "/etc/config"
		}
	]
}
```

## Kubectl token and config <a href="#6-toc-title" id="6-toc-title"></a>

DuploCloud provides you JIT token (15 minutes) to access the kubectl cluster. You can get the temporary token and the k8 cluster URL from the Infrastructure you created. Select the **Infrastructure** > **EKS** tab. Once you have the token and URL run the following commands locally

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

With these commands you have configured kubectl to point and access the k8 cluster. You can now apply the deployment templates by running the following command

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

If you want longer duration tokens you can create them on your own and secure them out of band from DuploCloud.

## Services display <a href="#7-toc-title" id="7-toc-title"></a>

Once the deployment command runs successfully, go to the **Services** tab of the Tenant. You can see those deployments. Now you can attach the load balancers for the services.



## Load balancers, WAF and other workflows <a href="#8-toc-title" id="8-toc-title"></a>

These all remain the same. See prior sections on creation of these.

## Adding Ingress <a href="#7-toc-title" id="7-toc-title"></a>

Once the Services are deployed and Service load balancer is created successfully, go to the **Ingress** tab.\
\
You can create Ingress and add rules. DuploCloud provides support to define multiple paths in ingress.

![](<../../../.gitbook/assets/image (14) (1).png>)

## ECS Fargate <a href="#9-toc-title" id="9-toc-title"></a>

Documentation TBD. Please [contact the DuploCloud team](https://duplocloud.com/company/contact-us/) for assistance.
