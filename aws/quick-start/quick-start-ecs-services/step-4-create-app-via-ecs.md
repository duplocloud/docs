# Step 4: Create app (via ECS)

You can enable ECS Cluster Under the Infrastructure -> ECS tab. We have already enabled ECS Cluster while creating Infrastructure at [Step 1](../step-1-infrastructure.md).

You can view the ECS Cluster name under ECS Tab (Under Infrastructure)

### Create Task Definition

We need to create a Task Definition prior to creating a service.

Switch the Tenant to DEV01.

Goto DevOps -> Containers -> ECS.

Create a Task Definition by giving the details below:\
**Name**: Task definition name. A task definition is required to run Docker containers in Amazon ECS.

**Image**: Provide the name of the image. In this example, we would be deploying httpd:latest

**vCPUs** and **Memory**: defines the image to be used, CPU, and memory requirements. In this example, we would be specifying 0.25 vCPU and 0.5 GB for the test application.

**Port Mappings**: Port mappings allow containers to access ports on the host container instance to send or receive traffic. In this example, we will specify port as 80.

<figure><img src="../../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

### Create ECS Service and Load Balancer

Next step is to configure ECS Service. Creating ECS Service creates a task that is expected to run until an error occurs or a user terminates it in the ECS Cluster.

Click on the details of Task Definition. You will see **Configure ECS Service**, click this link to create a service.

Provide below details:\
**Name**: In this example, we will provide input as sample-httpd-app.

Create a Load Balancer Listener for the port specified in the Task Definition (we will be specifying port as 80). Your input should look as the below image.

<div align="left">

<figure><img src="../../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

</div>

Submit the ECS service. It takes a few minutes to create the service.

