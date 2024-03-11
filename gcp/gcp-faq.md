---
description: Popular and frequently asked questions about DuploCloud and GCP
---

# GCP FAQ

## My Kubernetes service was stuck in “pending” for several minutes waiting to start a new pod. After that, it was able to start and stop pods quickly. What happened?

DuploCloud runs Kubernetes services in GCP on GKE in “autopilot” mode. Autopilot dynamically provisions nodes as needed to run your pods. This can add a couple of minutes to pod start time, similar to when Cluster Autoscaler dynamically adds hosts. You may see warnings from Kubernetes about being unable to place pods while autopilot hosts are starting, but they’ll clear once the hosts are available.

## How do I add a certificate to an internal load balancer?

Instructions need to be written. You can’t use Google Managed certs (at least not at the time this was written). You can either get a cert from somewhere else and import it or you can use a self-signed one. The self-signed option is reasonable for internal LBs because you control authentication at the IP level. It’s a little fiddly to do. We have Terraform that can be used as a reference.

## How do I grant a user access to only one Tenant in my GCP project?

Right now we don’t have JIT support for GCP. Users are given access to GCP projects directly in those projects.&#x20;

## One or more of my containers are showing in a pending state, how can I debug? <a href="#id-7-toc-title" id="id-7-toc-title"></a>

[Click here for the details](../aws/aws-faq.md#7-toc-title)

