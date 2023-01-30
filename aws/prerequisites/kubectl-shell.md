# Shell Access

DuploCloud allows shell access into the deployed containers. The way shell access is enabled is different based on the type of the system,  Native vs EKS

### Access to Native container shell

To enable shell for DuploCloud native container system, goto Devops->Container/EKS/Native and click on "Enable Docker Shell". Select a certificate from the drop down, and keep the Visibility to Public. This will provision a new service called _dockerservices-shell_ which will now enable the ability to SSH into the containers of the services.

<figure><img src="../../.gitbook/assets/Screen Shot 2022-04-15 at 10.28.01 AM.png" alt=""><figcaption></figcaption></figure>

### Access to Kubectl shell (K8s) and ECS Task shell

This is an optional feature where DuploCloud provides easy just-in-time access to the container shell and Kubectl shell directly from the browser. For this functionality to work we need to deploy a service in the Default tenant.

In the DuploCloud Portal, Switch the tenant to `default` from the top panel Tenant drop down.

Go to Devops --> Hosts --> Add. Give the following inputs

* Name: host01
* Instance Type: t2.small
* Image ID: Choose any image name that starts with Duplo-Docker. It might already be the default
* Agent Platform: Linux Docker / Native

Launch the VM and wait for it to be connected. Then we need to create a new service.

&#x20;Go to Devops --> Containers --> EKS/Native and click on add. Give the following inputs

* Name: `duplo-shell`
* Image: `duplocloud/shell:terraform-kubectl-v19.1`
* Replicas : `1`
* Platform : `Linux Docker / Native`
* Environmental variables

```
{
  "AWS_ACCESS_KEY_ID": "",
  "AWS_SECRET_ACCESS_KEY": "",
  "AWS_DEFAULT_REGION": "us-west-2",
  "EXPORT_BUCKET": "",
  "FLASK_APP_SECRET": "b33d13ab-5b46-ss3d-a19d-4sdds43",
  "DUPLO_AUTH_URL": "https://<DuploPortalUrl>"
}
```

Where DUPLO\_AUTH\_URL is the URL of the DuploCloud portal as you can see in the browser address bar. Leave all other forms as default.

Now we need to expose this service through an ELB. Under DevOps -->Containers-->EKS/Native click on the service called `duplo-shell` that you created above. Inside that confirm that the container is running. Then click on the load balancer tab and add a new one with the following input

* Select Type: Application
* Container Port: 80
* External Port: 443
* Visibility: Public
* Application Mode: Docker
* Health Check: /duplo\_auth
* Backend Protocol HTTP
* Certificate: This should be the certificate you added in the previous step

After completing this configuration, you can start using K8s shell from the portal for K8s services by clicking on KubeCtl Shell option.

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption><p>access KubeCtl Shell</p></figcaption></figure>

This configuration also enables users to view the  ECS task shell. This option is available under DevOps --> Containers --> ECS --> Tasks. Under Actions menu, click on ECS Task Shell. A browser will be launched to access the task shell further.

<figure><img src="../../.gitbook/assets/image (5) (2).png" alt=""><figcaption></figcaption></figure>
