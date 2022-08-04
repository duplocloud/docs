# Step 5: Create app (via K8S)

{% hint style="info" %}
DuploCloud supports three container orchestration technologies to deploy containerized applications in AWS. EKS, ECS Fargate and a built-in Container orchestration. If you don't care how the containers are deployed then you are not required to have Kubernetes or ECS expertise or even familiarity. But familiarity with Docker itself is indeed desired\
DuploCloud exposes a simple application specific interface to Deploy, update and debug containerized application.
{% endhint %}

A docker based application has by-and-large the following main specifications:

* **Name (Mandatory)** for the service
* **Docker image (Mandatory)**: for example nginx:latest. If the docker image is not in ECR, then you need to add the credentials for the docker registry under Devops-->Containers->EKS/Native-->Docker Credentials button
* **Replicas (Mandatory)**: In this demo, we will deploy a simple Hello World NodeJS web app. DuploCloud pulls Docker images from Docker Hub. You can choose a public image or provide credentials to access your private repository. For the sake of this demo, we will use a ready-made image available on Duplo’s repository on Docker Hub.

![](<../../.gitbook/assets/image (12) (1).png>)

* **Env Variables**: These are optional and you can pass environment specific values in this like DB host, port etc. For testing purposes you can also pass credentials in this
* Many other parameters which help ? icon in the UI against each input element in the form describing the purpose.\


![](<../../.gitbook/assets/image (14) (1) (1).png>)

To create a service go to Devops->Containers->EKS/Native and click on **+ADD** button and fill in the above field.

![](https://duplocloud.com/wp-content/uploads/2021/11/N1-service.png)

Press create and wait a moment for the service to initialize and you should see the containers running
