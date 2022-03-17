# Kubectl Shell

This is an optional feature where DuploCloud provides easy just-in-time access to container shell and Kubectl shell directly from the browser. For this functionality to work we need to deploy a service in the default tenant.

In the DuploCloud Portal, switch the tenant to be default in the top panel Tenant drop down. Go to Devops --> Hosts --> Add. Give the following inputs

* Name: host01
* Instance Type: t2.small
* Image ID: Choose any image name that starts with Duplo-Docker. It might already be default
* Agent Platform: Linux Docker / Native

Launch the VM and wait for it to be connected. Then we need to create a new service. Go to Devops --> Containers --> EKS/Native and click on add. Give the following inputs

* Name: duplo-shell
* Image: duplocloud/shell:terraform\_kubectl\_v15
* Replicas : 1
* Platform : Linux Docker / Native
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

Where DuploPortalUrl is the url of the DuploCloud portal as you can see in the browser address bar. Leave all other forms as default

Now we need to expose this service through an ELB. Under Devops-->Containers-->EKS/Native click on the service called duplo-shell that you created above. Inside that confirm that the container is running. Then click on the load balancer tab and add a new one with the following input

* Select Type: Application
* Container Port: 80
* External Port : 443
* Visibility: Public
* Application Mode: Docker
* Health Check: /duplo\_auth
* Backend Protocol HTTP
* Certificate: This should be the certificate you added in the previous step
