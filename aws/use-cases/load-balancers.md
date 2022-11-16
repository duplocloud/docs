# Load Balancers

Duplo Cloud provides the ability to configure Load Balancers with type Application Load Balancer, Network Load Balancer, and Classic Load Balancer.

Load Balancers can be configured for Docker Native, EKS Enabled, and ECS Services from DuploCloud Portal.

### Listener Rules using Shared Load Balancers

Applications can have distributed microservices where the requests need to serve on the basis of the path to the multiple services and route the traffic based on the application URLs. These rules provide us with a way to achieve this usecase.

#### Path-Based Routing <a href="#2d32" id="2d32"></a>

You can set the path-based rule as follows in your application load balancer listener rules.

Firstly create a Target Group for your service. You can create a **Target Group** from Docker Native, EKS Enabled, and ECS Services based on your application requirement.  Configure it from your Service, LoadBalancer Tab.

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

Once successfully created, Create  `Application Load Balancer` from **Networking** > **Load Balancer**.&#x20;

Note: Rules are not supported for Network Load Balancers.

Add the Target Group created in **** the prior step under the Listeners Tab. You can start adding routing rules for this listener now by clicking on the Actions --> **Manage Rules** option.

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

Add Routing Rules by specifying Rule Type, Values, and Forward Target Group.\
Forward Target Group lists all the Target Groups created for Docker Native, K8s, and ECS Services.

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

You can create multiple routing rules. Details of all the Routing Rules can be viewed/edited/deleted from the screen below.

<figure><img src="../../.gitbook/assets/image (22) (2).png" alt=""><figcaption></figcaption></figure>
