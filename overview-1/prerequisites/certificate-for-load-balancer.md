---
description: This step will be performed in GCP console
---

# Certificate for Load Balancer

The applications that will be deployed in the GCP environment will need to be exposed with SSL. In order to do that we need to provide GCP with certificate that can be used for loadbalancers and GKE ingress. We recomend that this certificate is issued for the wild char domain of the hosted zone we created in the previous step. For example if the DNS zone was apps.acme.com then the certificate would be for \*.apps.acme.com. Further we may choose to add multiple other domains to the certificate as those DNS names maybe different than the internal zone we created in the previous step.

1. Get a public cert and private cert files from your desired provider like GoDaddy or Namecheap.
2. Login to GCP console and naviage to "certificate manager" and click on classic certificates.\
   ![](<../../.gitbook/assets/image (432).png>)
3. We now need to create a global certificate for public facing load balancer and a regional certificate for private / internal load balancers. A load balancer could be an ingress as well.
   1. A global certificate can be created via the GCP console UI. Click on Create SSL certificate, give a name, public key and private key. note down the name of the global certificate. **It is a good practice to name it as global-\<DNS Domain name (with . replaced with -) created in the Cloud DNS Zone step>**\
      ![](<../../.gitbook/assets/image (433).png>)
   2. To create a regional certificate we need to open the GCP shell by clicking on the cloud shell icon on the top right corner of your GCP console. Once the shell opens. Create a file called public.cert and paste the content of the public certificate you have, then create a file called private.key and paste the content of the private key. Next we need to run the following command to create a regional. It is a good practice to name the regional certificate as \<regionname>-<**DNS Domain name (with . replaced with -) created in the Cloud DNS Zone step**>\
      _gcloud compute ssl-certificates create uscentral1-internal-acme-com --certificate=chain.crt --private-key=key.pem --region=us-central_  \
      As a best practice we name the certificate by prefixing the region and suffixing the domain name but replacing dot with dashes. Once the above command is run we should be able to refresh the page and now under classic certificate we would see 2 certificates. \
      We will reference these certificate names .

Note down the names of the certificates created as we will reference these names in the DuploCloud platform. Login to DuploCloud portal. Navigate to administrator --> Plans --> Certificate and add the 2 certificates. You can name them same as the names in GCP portal. Choose the type as LB SSL Certificate

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
