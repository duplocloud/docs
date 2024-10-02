# First Infrastructure Setup

Once the GCP project has been added to the DuploCloud portal, we setup the first infrastructure with a GKE standard cluster. Navigate to Administrator --> Infrastructure and add a new one. Give a name like nonprod; choose the project for Account; give a VPC CIDR say 10.30.0.0/16 (Kubernetes is IP Address hungry so give a /16 if you can); GKE standard is typically cheaper than auto pilot. Rest can be left as default. For production the visibility should be set to private



<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

This will take about 15-20 mins for the setup to complete. Keep an eye on faults to see if something is amiss. There maybe an occasional NTP clock sync fault that can be ignore. You will see in the Infrastructure status that it progresses from one state to another. When complete, then navigate to Administrators and Plans and you will see a plan with the same name as infrastructure.
