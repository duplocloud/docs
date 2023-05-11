# Step 6: Create a Load Balancer

All containers are running inside a private network and cannot be accessed external to the network. To do so, one can create a load balancer. The key fields in the load balancer form are

* Type: Select Application Load Balancer.
* Container Port: This is the port on which the application running inside the container is running. In this quick start we used duplocloud/nodejs-hello:latest, Container Port for sample application is 3000.
* External Port: This is the port we want the users to access the application. We will choose 80 because we are going to apply a certificate to the LB
* Application Mode : Choose Docker
* Health Check : use / for this case because the sample app returns 200 OK at this path.
* Certificate: Choose a certificate that was created as described in the [Prerequisites](https://docs.duplocloud.com/docs/aws/prerequisites/acm-certificate) section&#x20;

Go under Devops-->Containers --> EKS/Native and click on the service we are creating. Under that click on the Load balancer tab and configure the load balancer



<div align="left">

<figure><img src="../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

</div>

In about 2-3 minutes you will see the load balancer DNS names.&#x20;
