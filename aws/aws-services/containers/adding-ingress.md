# Adding Ingress

### Step1: Create Services with K8s NodePort

Navigate to **DevOps** > **Containers** > **EKS/Native** > **Services**

Create Service with **K8s Node Port**. These services would be configured in the K8s Ingress.

Example:

Let’s create three services to demonstrate how the Ingress routes our request. We’ll run nginx web applications with different paths.

![Services Page](<../../../.gitbook/assets/image (16).png>)

### Step2: Create K8s Ingress

Once Service and NodePort are successfully configured, you need to configure Ingress.

If in Infrastructure ALB Ingress is not enabled. Prior to following this step, Administrator need to enable the controller for your infrastructure.

**Admin** > **Infrastructure** > Select your Infrastrcuture > **Settings** > set _Enable ALB Ingress Controller_ property as `True`

Click on **K8s Ingress** Tab.

Create Ingress by defining rules to be configured for the services

![K8s Ingress Tab](<../../../.gitbook/assets/image (57).png>)

\
\
Example:

Here we have defined an Ingress to route requests to `/path1`for the first service, and requests to `/path2` for the second service. For the third service, we have provided a host, here the rules apply only to that host.

&#x20;Check out the `Ingress rules` table that declares how requests are passed along.

![Ingress Page](<../../../.gitbook/assets/image (13) (4).png>)

### Step3: View Ingress

Once Ingress is configured, you can access the Services configured based on the ingress rules using **DNS**

![K8s Ingress Tab](<../../../.gitbook/assets/image (18).png>)

Example:  Based on the Ingress rules configured for the three services, you can see the output results are different. Services configured are accessed based on the DNS specified in the DuploCloud Portal and the paths configured in Steps2.

> ``\
> `>curl http://sample-ingress.qaapps.duplocloud.net/path1/` \
> `this is service1`\
> ``\
> `>curl http://sample-ingress.qaapps.duplocloud.net/path2/` \
> `this is service2`\
> \
> `>curl -H "Host: example.com" http://sample-ingress.qaapps.duplocloud.net/ this is service3`
