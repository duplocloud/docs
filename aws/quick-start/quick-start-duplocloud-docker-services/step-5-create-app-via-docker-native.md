# Step 5: Create app (via docker native)

To create a service go to Devops -> Containers -> EKS/Native and click on **+ADD** button and fill in the above field.

**Name (Mandatory)** for the service

**Docker image (Mandatory)**: for example nginx:latest

**Platform**: Linux Docker/ Native

**Docker Networks**: Docker Default

**Env Variables**: These are optional and you can pass environment specific values in this like DB host, port, etc. For testing purposes, you can also pass credentials in this.

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

Press create and wait a moment for the service to initialize and you should see the containers running.

Once the Service is in Running status, you can also check the container logs from Containers Tabs --> Actions --> Logs.\
