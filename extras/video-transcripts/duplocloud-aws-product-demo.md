# DuploCloud AWS Product Demo

View the full [DuploCloud AWS Product Demo](https://duplocloud.com/videos/#gallery-1) video.

## Transcript&#x20;

**NARRATOR:**

Let's look at a product demo. In this sample scenario, we've decided to deploy a few applications to AWS.

The architects have come up with this infrastructure blueprint for one of the applications we need to manage.

In the diagram, we see a dedicated VPC, two availability zones with public and private subnets in each, deployed in the US West region.

We need to provision Docker containers on AWS EKS. In addition, it functions on AWS Lambda to obtain a serverless model for the microservices.

MySQL Aurora database and S3 are the data stores, and the application is exposed to the internet via load balancer, protected by a Web Application Firewall.

Now that we've gone through the desired architecture, let's get to work by using DuploCloud's user interface to deploy the application.

We could also use DuploCloud's Terraform provider or API, but we'll focus on the UI For this demo.

We start by logging in, and as an admin, create the network infrastructure.

Behind the scenes, the platform will auto-generate the required AWS configuration and complete the setup. This includes the VPC, availability zones, and subnets.

We then move to deploy the application infrastructure.

The application is called Invoice, and we start by creating a logical workspace known as a Tenant, where both admins and the appropriate developers can access the finance network we just created.

Next, we're gonna switch to the Invoice application, where we'll create the various cloud services, starting with a virtual machine.

Notice that the user provides a high-level specification only. Behind the scenes, the platform will generate the security group, IAM role, instance profile, and other AWS configurations.

From here, we'll create an S3 bucket.

The platform auto-generates the IAM access policy for the host to access the S3 bucket.

Detailed security controls, such as encryption, public access block, logging, among others, are applied to meet the compliance requirements.

We can provision a SQL database. The software understands that in this case, it needs to generate security-group-based policies as a guest IAM.

We'll also set up backups, encryption, and other best practices behind the scenes.

With network and network infrastructure in place, we next move to deploy first the Docker-based microservice.

Here again, the user provides application-centric specifications while the software auto-generates Kubernetes and AWS configurations that include the deployment or stateful sets, node ports, Ingress controls, and other such infrastructure details.

The right set of access policies, security groups, ACLs, are applied.

It's important to note that the platform is performing all these actions with no presumptions about the application topology that is being asked to deploy, and many other functions are built into the platform.

For example, we can see a quick view of the container logs or access the shell of the running container itself.

Just in time access to kubectl is provided for more granular control and debugging.

Across the platform, you can easily click Console to access the various cloud services inside of AWS.

An example of a time we would wanna do this would be in order to upload a Lambda package to an S3 bucket, the first step in deploying our Lambda function.

Notice that the platform implicitly provides just-in-time access for users for AWS Console access with the right permission set.

There are no access permissions to manage manually.

After uploading the package, we specify the Lambda function parameters and the software will do the rest.

As we complete all of the infrastructure, and the application has been deployed, we can look to do a sanity test.

Our application works.

The platform has been performing other necessary tasks for the infrastructure.&#x20;

For example, several diagnostics functions are implemented by default.

Here we're gonna take a look at a metrics dashboard that has been set up using Prometheus, Grafana, and CloudWatch with no further user input required.

Leveraging Elasticsearch, logs are collected and segregated per Tenant and per Service.

Alerts for various infrastructure resources can easily be configured as well.

The platform is using tools like CloudWatch and Prometheus for this, allowing the user to simply specify the filters for each alert.

Similarly, there's a billing dashboard to track costs across cloud services or across applications.

Next, businesses in highly regulated industries need a security and incident management platform, and that comes built-in.

All configuration changes in the cloud infrastructure are detected, and the controls are applied.

Compliance dashboards are readily available for auditors.

Notice that all of this is set up without the user having to lift a finger.

There's an audit trail of all actions in an application-specific context.

Here we are showing the audit trail for the Invoice workspace.

Finally, there are various options to configure CI/CD for your daily code releases.

Everything that we've done through the UI today can also be done via Terraform.&#x20;

Here's the script for the current setup, deploying a fully secure and compliant Infrastructure underneath with a fraction of the code that would've otherwise had to be written and maintained.

Autonomous DevSecOps are the future of cloud automation.&#x20;

To learn more, visit duplocloud.com.
