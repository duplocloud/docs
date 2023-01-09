# Step 6: Create LoadBalancer

All containers are running inside a private network and cannot be accessed externally. To do so one can create a load balancer. The key fields in the load balancer form are

* Type: Select Application Load Balancer.
* Container Port: This is the port on which the application running inside the container is running. In this quick start we used nginx:latest, Container Port for sample application is 80.
* External Port: This is the port we want the users to access the application. We will choose 80 because we are going to apply a certificate to the LB
* Application Mode : Choose Docker
* Health Check : use / for this case because the sample app returns 200 OK at this path.
* Certificate: Choose a certificate that was created as described in the [Prerequisites](../../prerequisites/) section&#x20;

Go under Devops-->Containers --> EKS/Native and click on the service we are creating. Under that click on the Load balancer tab and configure the load balancer



<figure><img src="../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

#### Secure Load Balancer

&#x20;if you want to secure the load balancer created, you can follow the steps specified [here.](../quick-start-eks-services/step-7-secure-the-load-balancer.md)

#### Create DNS Name

Follow the instructions [here](../quick-start-eks-services/step-8-create-dns-name.md).&#x20;

For the example we follow in this guide, you should screen as below:

<figure><img src="../../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>
