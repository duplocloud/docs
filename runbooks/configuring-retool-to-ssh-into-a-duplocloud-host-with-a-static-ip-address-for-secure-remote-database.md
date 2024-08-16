---
description: >-
  Runbook to configure DuploCloud Hosts with a static IP and SSH database
  tunneling for secure remote access
---

# Configuring Retool to SSH into a DuploCloud Host with a Static IP Address for Secure Remote Database

This setup is useful in scenarios for DuploCloud customers with external users in remote locations who need consistent, secure access to databases Hosted on DuploCloud infrastructure. By configuring a public-facing DuploCloud Host and attaching an Elastic IP, you provide a stable and consistent endpoint for Retool to connect to. SSH tunneling is then used to create a secure, encrypted connection between Retool and the database through the DuploCloud Host. This approach ensures that even over the public internet, data transfers remain protected and private. By combining the static Elastic IP with SSH tunneling, you achieve reliable access and robust security for database interactions.

## Use this Runbook if….

Use this procedure if you are a DuploCloud customer who needs secure external access to your organization’s cloud resources for:

* **Public Availability with Security:** DuploCloud customers with external clients, vendors, or team members who need to interact with the database but cannot be given direct access for security reasons
* **Public Host Access with Strict Database Security:** Users who need external Host accessibility while maintaining secure strict security controls for databases.
* **Simplified Development Workflow:** Users with remote developers who need to connect to the environment without dealing with dynamic IP change and securely interact with the database for tasks like development, testing, or debugging, as if they were directly connected to the cloud network.
* **Secure Troubleshooting:** System administrators or support teams who need to quickly connect to the Host from anywhere or securely access and troubleshoot the database without exposing it to potential security risks.

## Prerequisites

* A DuploCloud Host with a Public IP and network access to your database.
* A Retool account.&#x20;

## Step 1. Attaching an Elastic IP to the DuploCloud Host

### Login to AWS Console

1. Navigate to [AWS Management Console](https://aws.amazon.com/).
2. Log in with your credentials.

### Allocate a New Elastic IP

1. In the AWS Console, navigate to the EC2 dashboard.
2. In the EC2 Dashboard, [Allocate an Elastic IP address](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/working-with-eips.html#using-instance-addressing-eips-allocating) connected with the appropriate network (VPC).

### Associate the Elastic IP with DuploCloud Host

1. Once the Elastic IP is allocated, select it from the list.
2. [Associate the Elastic IP address](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/working-with-eips.html) with your DuploCloud Host instance.

{% hint style="info" %}
An AWS account is needed to allocate and manage Elastic IP addresses because they are an AWS-specific service. If you're using a different cloud provider, create and associate a static IP with your DuploCloud Host using their equivalent static IP addressing service.
{% endhint %}

## Step 2. Configuring SSH Access

### Log in to Retool

1. Navigate to the [Retool login page](https://login.retool.com/auth/login?source=homepage).
2. Log in with your credentials.

### Configure SSH Tunneling

1. Follow the instructions to [Configure SSH tunneling](https://docs.retool.com/data-sources/guides/connections/ssh-tunnels#configure-ssh-tunneling), being sure to:

* Enter the public IP of your DuploCloud Host.
* Set the SSH port to 22 and configure it to use the private key you saved earlier.

## Step 3. Whitelisting the Retool IPs Addresses

### Log in to DuploCloud

1. Navigate to the DuploCloud Platform.
2. Log in with your credentials.

### Add Tenant Security Settings to Whitelist Retool IP Addresses

1. In the DuploCloud Portal, navigate to **Administrator** -> **Tenant**.
2. Select the Tenant where your host is running from the **NAME** column.
3. Select the **Security** tab and click **Add**. The **Add Tenant Security** pane displays.
4. Add the Retool IP addresses using the following inputs:

* **Source Type:** IP Address
* **IP CIDR:** Custom
* **IP Address:** Enter the [Retool CIDR IP Addresses](https://docs.retool.com/data-sources/reference/ip-allowlist-cloud-orgs) (and individual IP’s as needed).
* **Protocol:** TCP
* **Port Range:** 22

5. Click Add.&#x20;

## Summary of Steps

### 1. Attaching an Elastic IP to the DuploCloud Host

* Login to AWS Console
* Allocate a New Elastic IP
* Associate the Elastic IP with DuploCloud Host

### 2. Configuring SSH Access

* Log in to your Retool
* Configure SSH Tunneling

### 3. Whitelisting the Retool IPs Addresses

* Log in to DuploCloud
* Add Tenant Security Settings to Whitelist Retool IP Addresses

This Runbook configures secure SSH access from Retool to a DuploCloud Host by attaching an Elastic IP, setting up SSH tunneling, and whitelisting Retool IP addresses to ensure proper connectivity and security.

## Resources

Links to resources that may be helpful to users of this Runbook.&#x20;

[DuploCloud documentation for creating Hosts](https://docs.duplocloud.com/docs/overview/use-cases/hosts-vms/adding-hosts).
