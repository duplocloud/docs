# Quick start

## Introduction <a href="#0-toc-title" id="0-toc-title"></a>

Switch to the Tenant we have created. Deployment is a three-step process:

1. Creating Host (VM)
2. Deploying a Service
3. Exposing the service using LB

## Step 1: Create a host (VM) <a href="#1-toc-title" id="1-toc-title"></a>

From the menu navigate to **DevOps > Hosts > Azure > Azure Hosts > + sign** above the table. Choose the desired instance type. The available instance types are set by your administrator or the plan you choose in DuploCloud. If you are not using this host for hosting containers, then set the pool as none. If you want a public IP for the host, then enable the public IP.

![](https://lh4.googleusercontent.com/arxWKAmtdByf\_paHsCFY46JHywvq86ZR50Gec3\_60ZIV5yzoRLH9nE1MzaMeL6oEwdwiSJ2jL22QePMFhnj3LvkVbi8iPR7m3mN05XwbtOKv7uZ3XZZvPUqO5a\_zHNz4UtM8F\_Ya)

## Step 2: Deploy a service (application) <a href="#2-toc-title" id="2-toc-title"></a>

From the menu navigate to **DevOps > Services > + Sign** above the table. Give a name for your services (no spaces); number of replicas; Dockerimage; volumes (if any). The number of replicas must be less than or equal to the number of hosts in the fleet.

![](https://duplocloud.com/wp-content/uploads/2021/11/createrole.png)

## Step 3: Expose using LB <a href="#3-toc-title" id="3-toc-title"></a>

Create an LB from the menu **DevOps > Services > + Sign** above the table for Load Balancer Configuration. The URL suffix you specify under Health Check will be used by DuploCloud during rolling upgrade i.e., when a service image is changed then DuploCloud will take down one container replica at a time and bring up a new one, then once it is running the DuploCloud agent running on the host will make a call to the URL and expects a 200 OK. If it does not get a 200 OK then the upgrade is paused and the user needs to update with an image that fixes the issue.

![](https://duplocloud.com/wp-content/uploads/2021/11/createelb.png)

The DNS name for the service will be present in the Services Table. It takes about 5 to 10 minutes for the DNS name to start resolving.

Update a Service from the menu **DevOps > Services > Select** the service from the table and click on edit.
