---
description: Common questions about using DuploCloud GCP
---

# GCP FAQs

### My Kubernetes service was “pending” for several minutes, waiting to start a new pod. After that, it was able to start and stop pods quickly. What happened?

DuploCloud typically runs Kubernetes services in GCP on GKE in Autopilot mode. Autopilot dynamically provisions nodes as needed to run your pods. This can add a couple of minutes to the pod start time. You may see warnings from Kubernetes about being unable to place pods while autopilot hosts are starting, but they’ll clear once the hosts are available.

### One or more of my containers are showing as pending; how can I debug them? <a href="#id-7-toc-title" id="id-7-toc-title"></a>

[Click here for the details](../aws-user-guide/aws-faq.md#7-toc-title)

### How do I grant users access to only one Tenant in my GCP project?

To give a user access to a specific Tenant, navigate the Users page. For a new user, click Add and enter the user's information. From the Role list box, select User. When the user role is selected, the Tenant list box displays. In the Tenant list box, select the Tenant(s) you would like to give the user access to. Click Submit. For an established user, navigate to the Users page and select the name of the user whose access you would like to update. From the Actions menu, click Update. From the Role list, select User, and from the Tenant list box, select the Tenant(s) to which you want to give them access. Click Submit.&#x20;

### How do I create a Google Managed certificate for use with DuploCloud?&#x20;

To create a Google Managed certificate for use with DuploCloud, see the DuploCloud documentation on [creating managed certificates with GCP](../overview-1/prerequisites/create-managed-ssl-certificates-for-gcp.md).

