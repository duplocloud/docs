# Step 6: Create a Load Balancer

All containers are running inside a private network and cannot be accessed from outside. To do so one can create a load balancer. The key fields in the load balancer form are

* Type: Classic or Application. Classic is deprecated by AWS so we will choose Application
* Container Port: This is the port on which the application running inside the container is running. In this quick start we used nginx:latest so it will be 80
* External Port: This is the port we want the users to access the application. We will choose 443 because we are going to apply a certificate to the LB
* Application Mode : Choose Docker
* Health Check : use / for this case because the nginx image returns 200OK at this path.
* Certificate: Choose a certificate that was created as described in the [Prerequisites](../prerequisites/) section&#x20;

Go under Devops-->Containers --> EKS/native and click on the service we are creating. Under that click on the Load balancer tab and configure the load balancer



![](<../../.gitbook/assets/image (11) (1).png>)

In about 2-3 minutes you will see the load balancer DNS names.&#x20;



