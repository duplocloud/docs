---
description: Set up Pulumi to manage infrastructure using the DuploCloud provider
---

# Getting Started with Pulumi for DuploCloud

DuploCloud supports [Pulumi](https://www.pulumi.com/docs/) as a modern Infrastructure-as-Code (IaC) tool that lets you define cloud infrastructure using familiar programming languages like Python or TypeScript. By using DuploCloud’s native Pulumi provider, you can interact directly with the DuploCloud API to provision Tenants, cloud services, and applications across AWS, Azure, and GCP, without writing any native cloud provider code.

## Prerequisites

Before getting started with Pulumi and DuploCloud, make sure you have the following:

* A DuploCloud portal and API token ([How to create an API token](../access-control/api-tokens.md)).
* Familiarity with [Pulumi concepts like stacks and projects ](https://www.pulumi.com/docs/iac/concepts/projects/)(helpful but not required).

## Step 1: Install the Pulumi CLI

To run and deploy Pulumi programs, install the Pulumi CLI using this command:

```bash
curl -fsSL https://get.pulumi.com | sh
```

Verify the installation:

```bash
pulumi version
```

For platform-specific instructions, see the [official Pulumi installation guide](https://www.pulumi.com/docs/iac/download-install/).

## Step 2: Set Up Your DuploCloud Environment

Set environment variables to allow Pulumi to authenticate with the DuploCloud API and target the correct portal:

```bash
export DUPLO_HOST="https://myportal.duplocloud.net"
export DUPLO_TOKEN="your_api_token_here"
```

## Step 3: Initialize a Pulumi Project

Create a new directory for your Pulumi project, and initialize it:

```bash
mkdir duplocloud-pulumi-demo
cd duplocloud-pulumi-demo
pulumi new aws-python  # or your preferred template/language
```

This sets up a basic Pulumi project structure.

## Step 4: Install the DuploCloud Pulumi Provider

Install the DuploCloud provider for your selected language:

### **Python**

```python
pip install pulumi-duplocloud
```

### **JavaScript/TypeScript**

```javascript
npm install @duplocloud/pulumi
```

### **Go**

```go
go get github.com/duplocloud/pulumi-duplocloud/sdk/go/...
```

### **.NET**

```aspnet
dotnet add package DuploCloud.Pulumi
```

## Step 5: Write and Deploy Your Pulumi Program

Define your infrastructure using Pulumi code with the DuploCloud provider. For example, you can:

* Create Tenants
* Provision Kubernetes clusters
* Deploy DuploCloud services and resources

Then deploy your stack using this command:

```bash
pulumi up
```

Follow the prompts to review and confirm the changes.

## Step 6: Manage Your Pulumi Stack

Use the following Pulumi commands to manage your deployment lifecycle:

```bash
pulumi preview   # Simulate a deployment and review proposed changes
pulumi stack     # Show the current stack’s name, outputs, and config
pulumi destroy   # Remove all resources created by this Pulumi stack
```

## Additional Resources

* [DuploCloud Pulumi GitHub Repository](https://github.com/duplocloud/pulumi-duplocloud) – Code samples and provider documentation
* [Pulumi Documentation](https://www.pulumi.com/docs/) – Reference for general Pulumi usage
* [DuploCloud API Tokens](../access-control/api-tokens.md) – How to create and manage your API tokens
